# Tortuga

## Challenge Overview
- **Original French description:** On vous propose une séance de dessin !

    Le fichier tortuga-flag.txt contient le flag dessiné uniquement à l'aide de segments.

    La méthode pour encoder ces segments est simpliste. On fixe un point de départ P(x, y) initialisé à un point quelconque dans le plan, par exemple (0, 0). Puis, chaque élément (dx, dy) dans la liste L fournie dans le fichier tortuga.txt permet d'atteindre un nouveau point Q(x + dx, y + dy) et le segment PQ est tracé entre ces deux points. Une fois ce segment tracé, le point courant P est remplacé par le point Q, et ce procédé est itéré sur tous les éléments de la liste.

    Afin d'autoriser plusieurs symboles, la valeur spéciale (0, 0) pour (dx, dy) est utilisée pour déplacer le point P comme décrit ci-dessus avec l'élément suivant de la liste, mais aucun segment n'est tracé.

    On donne l'exemple suivant (tortuga-example.txt) où le point initial P est choisi tout en haut à gauche.

    ```bash
    [
        # Draw triangle pointing down (drawn clockwise)
        (2, 0), (-1, 2), (-1, -2),
        # Skip
        (0, 0), (3, 0),
        # Draw triangle pointing up (drawn counterclockwise)
        (-1, 2), (2, 0), (-1, -2),
        # Skip
        (0, 0), (1, 0),
    ] * 6
    ```

- **Translated Description :** You are offered a drawing session!

    The file tortuga-flag.txt contains the flag drawn solely using segments.

    The method to encode these segments is simplistic. A starting point P(x, y) is fixed, initialized to any point in the plane, for example (0, 0). Then, each element (dx, dy) in the list L provided in the file tortuga.txt allows reaching a new point Q(x + dx, y + dy), and the segment PQ is drawn between these two points. Once this segment is drawn, the current point P is replaced by point Q, and this process is iterated over all elements of the list.

    To allow for multiple symbols, the special value (0, 0) for (dx, dy) is used to move point P as described above with the next element of the list, but no segment is drawn.

    The following example (tortuga-example.txt) is given where the initial point P is chosen at the top left.

<div align="center">
  <a href="images/tortuga-example.png"><img src="images/tortuga-example.png" alt="Puzzle" width="600"></a>
</div>


## Solution

```bash
pip install pillow
pip install imageio

```

```Python
from PIL import Image, ImageDraw
import os
import imageio


import subprocess

# Command to run
command = "rm -r frames"

# Run the command
process = subprocess.Popen(command, shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
# Command to run
command = "mkdir frames"
process = subprocess.Popen(command, shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE)

def trace_segments(liste_tuples, foldername):
    # Initialisation du point de départ à (0, 0)
    x, y = 0, 0
    
    # Liste pour stocker les coordonnées des points visités
    points = [(x * 10, y * 10)]
    
    # Création du dossier pour stocker les images
    os.makedirs(foldername, exist_ok=True)
    
    # Création d'une image blanche
    img = Image.new('RGB', (800, 50), color='white')
    draw = ImageDraw.Draw(img)
    should_skip_next = False
    # Parcours de la liste de tuples
    for i, (dx, dy) in enumerate(liste_tuples):
        # Si le déplacement est nul, passer au prochain tuple
        
        
        # Calcul du nouveau point
        x += dx * 10
        y += dy * 10
        
        
        
        if dx == 0 and dy == 0:
          draw = ImageDraw.Draw(img)
          print("heree")
          draw.line([(points[-1][0], points[-1][1]), (x , y )], fill='white', width=2)
          should_skip_next = True
          continue
        elif should_skip_next :
          points.append((x , y ))
          should_skip_next = False
          continue
        else :
          should_skip_next = False
          # Ajout des coordonnées du nouveau point dans la liste
          points.append((x , y ))
          # Tracé du segment entre le point courant et le nouveau point
          draw.line([(points[-2][0], points[-2][1]), (x , y )], fill='black', width=2)
        
        # Sauvegarde de l'image
        img.save(os.path.join(foldername, f"frame_{i:03}.png"))
    
    # Création de l'animation GIF
    images = []
    for filename in sorted(os.listdir(foldername)):
        images.append(imageio.imread(os.path.join(foldername, filename)))
    imageio.mimsave('segments_animation.gif', images, duration=100)

# Lire les instructions de dessin à partir du fichier
with open('tortuga-flag.txt', 'r') as file:
    liste_tuples = eval(file.read())

# Appel de la fonction pour tracer les segments et créer l'animation GIF
trace_segments(liste_tuples, 'frames')

```

![Alt Text](images/segments_animation.gif)


**Flag**: FCSC{316834725604}