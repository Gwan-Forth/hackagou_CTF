![bel_oiseau](bel_oiseau.png)

![fichier_bel_oiseau](fichier_bel_oiseau.txt)
## Résolution

Le fichier texte contient une image encore faut-il pouvoir le lire.

Quand on regarde le début et la fin du fichier, on voit que ça ne correspond pas aux en-tête par défaut des images, idem pour la fin du fichier.

Par contre en y regardant de plus près la fin du fichier : `e40598` et en inversant cette chaine : `89504e`.

Si on la compare dans la liste des signature des types de fichiers : https://en.wikipedia.org/wiki/List_of_file_signatures on se rend compte que c’est l’en-tête d’un png ! 

A partir de là c’est simple : 
* inverser toute la chaine du fichier
* convertir le hex
* écrire le tout dans un fichier de sorti pour avoir notre image

On fait ça avec un script en python : 
```python
with open('./fichier_bel_oiseau.txt', 'r') as file:  
    data = file.read()  
  
with open('./output.png', 'wb') as output:  
    output.write(bytes.fromhex(data[::-1]))
```

>[!question]- Spoiler du flag
> OPENNC{Airc4l1n}

