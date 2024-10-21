> Vous êtes sur le point de terminer Tchia, le jeu qui vous plonge au coeur même de la Nouvelle-Calédonie. Alors que vous atteignez un moment crucial, vos parents, excédés de vous voir jouer si longtemps, décident de couper le courant. L’écran s’éteint brutalement, et vous vous résignez à tout perdre. Mais à la surprise générale, lorsque vous rallumez la console, le jeu est corrompu : des bugs graphiques, des textures manquantes, et surtout... des images étranges apparaissent de manière aléatoire.
> 
> Ces "glitches" ne semblent pas être de simples erreurs visuelles. À chaque nouvelle image, des symboles apparaissent, comme des fragments d’un message ancien. Vous remarquez que chaque image contient une partie d’un grand puzzle.
> 
> Format du flag : OPENNC{quelque_chose}
> 
> Auteur : Ketsui


![challenge](../../../../attachements/challenge.zip)
## Résolution

Le zip contient tout une série d’image nommé `n_X_Y.png`.
Quand on les regardes à la suite on ne comprends pas grand chose, mais ce qu’on sait c’est que ces images sont une partie d’un tout.

Et si on prend un peu de temps pour comprendre la nomenclature, on peux supposer que la position de chaque pièce dans l’image d’origine est indiqué dans le nom.

Maintenant comment les recoller toutes ensemble ? Et bien on peux demander à chatgpt : `j'ai plusieurs image qui sont des bout d'un ensemble comment faire pour reconstituer l'image de base sachant que les fichies sont nommés du genre n_0_1.png le premier chiffre représentant le X et le deuxième le Y de l'image dans l'image finale`

Et il nous sort le script suivant :

```python
from PIL import Image
import os
import re

def reconstituer_image(image_folder, output_image):
    # Charger toutes les images dans le dossier
    images = {}
    for img_file in os.listdir(image_folder):
        if img_file.endswith(".png"):
            # Extraire les coordonnées X et Y du nom de fichier
            match = re.match(r"n_(\d+)_(\d+)\.png", img_file)
            if match:
                x, y = int(match.group(1)), int(match.group(2))
                img_path = os.path.join(image_folder, img_file)
                images[(x, y)] = Image.open(img_path)

    # Trouver les dimensions de l'image finale
    x_max = max(x for x, y in images.keys())
    y_max = max(y for x, y in images.keys())

    # Obtenir la taille d'un morceau (elles doivent toutes avoir la même taille)
    img_width, img_height = images[(0, 0)].size

    # Créer une nouvelle image vide avec la taille totale
    total_width = (x_max + 1) * img_width
    total_height = (y_max + 1) * img_height
    new_image = Image.new('RGB', (total_width, total_height))

    # Parcourir les morceaux et les coller dans la nouvelle image aux bonnes coordonnées
    for (x, y), img in images.items():
        x_offset = x * img_width
        y_offset = y * img_height
        new_image.paste(img, (x_offset, y_offset))

    # Sauvegarder l'image reconstituée
    new_image.save(output_image)
    print(f"L'image a été reconstituée et sauvegardée sous le nom {output_image}")

# Utilisation
image_folder = "path_to_folder_containing_images"  # Dossier contenant les morceaux d'images
output_image = "final_image.png"  # Nom du fichier de sortie

reconstituer_image(image_folder, output_image)
```

A adapter bien sûr pour que le script puisse accéder aux images. Ce qui nous donne en résultat : 
![puzzle_final_image](../../../../attachements/puzzle_final_image.png)

On le lit en ligne pour se simplifier la vie avec un site comme https://scanqr.org/
Et on obtient : `https://youtu.be/FKynmIW5LIA`

Quand on va sur la page on se retrouve avec une vidéo qui dure 10 seconde et nous donne un message/indice :
`Tchia existe croyez moi et si vous  ne me croyez pas trouvez le flag, il faut parfois penser comme un  non-voyant pour réellement voir.`

Le message n’est pas vraiment clair, mais en gros, quand on a un handicap pour regarder une vidéo que ferait cette personne ?

La réponse ici : `activer les sous-titres`.

Du coup plusieurs solution :
* activer les sous-titres et regarder la vidéo, vous aurez le flag dans les 2 dernières secondes de la vidéo
* ne pas s’embêter, cliquer sur `Show more` sur youtube et `Show transcript`. Vous aurez tous les sous-titres de la vidéo directement, et rien de mieux pour copier coller le flag.

>[!tip] indice
>L’indice dans le transcript est beaucoup plus parlant : `il faut parfois écouter comme un  sourd pour réellement comprendre.`.Les organisateurs ont peut-être jugé trop facile et on modifié le message audio pour corser un peu.


>[!question]- Spoiler du flag
> OPENNC{Bravo_tu_as_trouve_Puzzle}


