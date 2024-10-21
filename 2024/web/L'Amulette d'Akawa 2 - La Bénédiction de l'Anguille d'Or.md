## Enoncé

>Après avoir franchi le premier sceau, tu arrives près d'une rivière souterraine où nage une anguille d'or, gardienne des eaux de la grotte. Une inscription est gravée sur la roche : "Seule la parole des sages peut ouvrir le passage."
>
>La bénédiction pour traverser la rivière repose sur une formule magique qui semble être authentifiée par un symbole, mais il te semble que ce dernier n'est qu'une illusion.
>
>Un mystérieux parchemin t'indique une série de symboles semblant former un message magique. Cependant, tu te rends vite compte que cette bénédiction a une faiblesse. Il te suffit de modifier discrètement ce message, sans même t'occuper des protections visibles, pour obtenir la bénédiction et traverser les eaux.


## Résolution

Ici on va se rendre sur l’URL donné avec firefox dans kali: `[http://challenges.hackagou.nc:5005](http://challenges.hackagou.nc:5005/)`

Si on ne passe pas par firefox ça ne fonctionnera pas car l’url est en HTTP uniquement et google chrome ne réagi pas bien à ça.

On va même aller plus loin et utiliser bupsuite pour suivre les échanges entre le client et le serveur.

On arrive sur le formulaire du site et on tente quelque chose par défaut : `admin:admin`.

Et on voit dans burpsuite après avoir soumis le formulaire qu’on a un cookie : `Cookie: auth=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZG1pbiI6MCwiZXhwIjoxNzI4MzM0MzEwfQ.wqBen_0yPEOXPLWSrpQnDC8Xtzcy0G9NyRXYB9I27eM`

A première vu, le cookie ne nous dit rien, mais si on le passe dans dcode identifier, on se rend compte que c’est du base64 un peu modifié et qu’on peux le déchiffrer.

En fait, le cookie est composé de trois partie et chacune est séparé par un point.

* la première partie indique l’algorithme pour le jwt : `{"alg":"HS256","typ":"JWT"}`
* le deuxième quelque chose qui nous intéresse : `{"admin":0,"exp":1728334252}`
* et le troisième c’est du binaire

En se référant au challenge précédent, on sait que pour passer il faut que le serveur sache que l’on est admin et donc que cette valeur soit à `1`.

Pour outrepasser la sécurité il faut donc que l’on se génère un cookie avec la partie du milieu équivalent à `{"admin":1,"exp":1728334252}`.

On encode ça en base 64 et ça nous donne : `eyJhZG1pbiI6MSwiZXhwIjoxNzI4MzM0MjUyfQo=`

Le signe `=` ne fait partie d’aucune chaîne donc on suppose qu’on doit les supprimer avant de les mettre dans les cookie ce qui nous donne `eyJhZG1pbiI6MSwiZXhwIjoxNzI4MzM0MjUyfQo`

Mit bout à bout on obtient donc le cookie : `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZG1pbiI6MSwiZXhwIjoxNzI4MzM0MjUyfQo.wqBen_0yPEOXPLWSrpQnDC8Xtzcy0G9NyRXYB9I27eM`

Il ne reste plus qu’à soumettre le formulaire, et remplacer la valeur du cookie à la volée et on accès à la page des admin.

>[!question]- Spoiler du flag
> OPENNC{Jw7_C'3s7_B13n,_s3cUr1s3_c'3s7_M13uX!!!}

