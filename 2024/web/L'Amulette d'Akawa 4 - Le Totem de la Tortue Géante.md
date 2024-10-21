![amulette_akawa_4](../../../../attachements/amulette_akawa_4.png)

## Enoncé

> Enfin, après avoir traversé de nombreux pièges, tu te retrouves face à la dernière épreuve. Le totem de la Tortue Géante se dresse devant toi, protectrice de l’amulette. L'inscription sur le totem est claire : "Seule la
> patience et la persévérance peuvent venir à bout de ma protection."
>
> Une nouvelle énigme magique apparaît, un symbole semblant inviolable, protégé par un mot de passe aussi ancien que les montagnes. Mais, à force d’observer et de comprendre, tu réalises que le mot de passe est faible, trop simple pour un gardien aussi puissant. En persistant et en déchiffrant cette dernière énigme, tu pourras enfin briser la protection et atteindre l'amulette d'Akawa.

## Résolution

Ici on suit le même procédé que [L'Amulette d'Akawa 3 - L'Illusion de la Chouette Nocturne](L'Amulette%20d'Akawa%203%20-%20L'Illusion%20de%20la%20Chouette%20Nocturne.md)

On utilise burpsuite, on fait un suivi des échange jusqu’à ce qu’on arrive à la partie jwt dans un cookie.

Et on récupère donc la chaine `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZG1pbiI6MCwiZXhwIjoxNzI4MzYyMzkzfQ.Iij-_jVG-FcHHYwFSdkkQrkzoJMsmS44K8YpqUdkB7g`.

L’énoncé est assez clair sur ce qu’on doit faire : 
* trouver le secret qui permet d’encoder les jwt
* faire un nouveau jwt valide qui nous donne les droits admin
* charger le jwt lors de la requête vers le site

Pour trouver le secret, [](../../../../ressouces/tools/Crack%20secrets.md#john) nous sera utile.
On met le jwt dans un fichier et on lance john : `john jwt.txt`

Le secret est vraiment simple : `123456789`

Avec ce secret il ne nous reste plus qu’à générer un jwt correcte , on va utiliser le site https://jwt.io/ qui est parfait pour ça, on envoi le jwt de base, on modifie la valeur pour admin et on signe le jwt :

![amulette_akawa_4_jwt](../../../../attachements/amulette_akawa_4_jwt.png)

On se retrouve donc avec `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZG1pbiI6MSwiZXhwIjoxNzI4MzYyMzkzfQ.21s53Rc8GL9dQejw0kc3qV1TZwSd4iC9-yBYMcaVhN0`

On le charge dans burpsuite et on accède à la page avec le flag.


>[!question]- Spoiler du flag
> OPENNC{Jw7_W0rk5_b3773r_w17h_57r0nG_K3y5}

