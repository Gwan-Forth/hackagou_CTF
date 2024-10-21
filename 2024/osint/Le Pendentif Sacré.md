"Il y a plus de 100 ans, une tribu de la mer nommée Araqtr brillait par sa puissance et sa navigation. Le Chef Arak portait un pendentif sacré dont la légende raconte qu'il lui apportait le pouvoir de guérison.

Cependant, un tel pouvoir suscitait d'innombrables haines et jalousies, même au sein de son propre peuple. Il décida donc de cacher ce pendentif. Seuls ses descendants, qui portaient toujours ces valeurs, connaissaient le code menant au trésor.

Au fil du temps, de génération en génération et par peur, les descendants continuèrent à garder ce secret, mais en y ajoutant de la complexité. Car même s'il devait être dévoilé, nul ne saurait l'exploiter.

Nous avons pu récuperer ce message caché...Il est temps de récuperer ce pendentif. Trouve son emplacement !

```
9M582222+22 
9H9R2222+22 
CHJP2222+22 
9M242222+22 
8MG92222+22 
9M3Q2222+22 
```

Format du flag : `OPENNC{emplacement}`

Sans maj sans accent et un underscore (_) pour les espaces. (taguez un modo si vous n'êtes pas sûr).

Exemples : `OPENNC{baie_des_citrons}` ou encore `OPENNC{ilot_maitres}`

## Résolution

```
9M582222+22 : 53.0000625,86.0000625 - Ovsyannikovo, Altai Krai, Russia
9H9R2222+22 : 57.000062,56.000062 - Antuf'evo, Perm Krai, Russia
CHJP2222+22 : 82.000062,54.000062
9M242222+22 : 50.000062,82.000062 
8MG92222+22 : 40.000062,87.000062 - xinjiang
9M3Q2222+22 : 51.000062,95.000062
```

On récupère les coordonnées : 
`53 86 57 56 82 54 50 82 40 87 51 95`

On l’envoi dans cyberchef qui nous indique qu’il y a moyen de faire quelque chose avec la recette `from decimal` et on trouve `5V98R62R(W3_`.

Cette chaine ne nous dit rien, mais il y a une erreur dedans : `(` est censé être un `+`.
Ce qui donne : `5V98R62R+W3_`, c’est du plus code en enlevant le dernier caractère.

On envoi dans `5V98R62R+W3` dans google maps et on tombe sur notre réponse.


>[!question]- Spoiler du flag
> OPENNC{ilot_rond}

