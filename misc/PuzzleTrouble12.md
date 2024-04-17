# Puzzle Trouble 1/2

## Challenge Overview
- **Original French description:** On vous demande de retrouver le flag dans ce bazar de tuiles ! Il paraît qu'elles n'ont pas été retournées...

- **Translated Description :** We ask you to find the flag in this tile bazaar! It seems that they have not been returned...

<div align="center">
  <a href="images/puzzle-trouble-easy.jpg"><img src="images/puzzle-trouble-easy.jpg" alt="Puzzle" width="800"></a>
</div>


## Solution

One approach is to use image processing libraries like OpenCV or PIL to detect rectangles based on border color similarity. You can iterate through the image pixels, identify contiguous regions with similar colors, and then fit rectangles around them. 



Alternatively, you can leverage existing tools like the GitHub project [gaps](https://github.com/nemanja-m/gaps) (Genetic Algorithm based solver for jigsaw puzzles). This tool automates the process of solving jigsaw puzzles by employing genetic algorithms and automatically detecting piece sizes.

We can clone this repository and install its requirements

Since we have an 1024x1024 image with 8 rectangle lines and 8 rectangles columns so each rectangle is 128x128

```bash
git clone https://github.com/nemanja-m/gaps.git

cd gaps

!pip install .

# You should copy the puzzle image into gaps folder
!gaps run puzzle-trouble-easy.jpg solution.jpg --generations=20 --population=600 --size=128
```


<div align="center">
  <a href="images/puzzle-trouble-easy-solution.jpg"><img src="images/puzzle-trouble-easy-solution.jpg" alt="Puzzle" width="800"></a>
</div>

You only have to rewrite the flag and submit it.