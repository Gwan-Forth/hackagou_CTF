
> Un ancien, que j'ai rencontré du côté de Nouré en train de pêcher à l'épervier, a été très gentil avec moi et on a bien discuté.
> 
> Voulant le revoir, je suis retourné les jours suivants voir vers où il pêche. Ne le voyant pas, j'ai tenté plusieurs fois, en vain.
> 
> Mais je sentais sa présence, et j'ai compris que c'était un Esprit, il me parlait dans ma tête. Il m'a indiqué un endroit, sur l'îlot - facilement accessible à pied à marée basse - "mais ne va pas au delà du cocotier, c'est là que j'ai vécu".
> 
> En y allant, j'ai remarqué un grand nombre de coquilles d'acatina, les escargots étaient morts et les coquilles propres. Chaque jour, il y a avait un tas, avec un nombre différent de coquilles vides.
> 
> Je lui demandais à chaque fois avec respect si je pouvais ramasser et compter ces coquilles. Il m'a répondu une fois : "décode ces nombres mon fils, tu connaîtras ma tribu d'origine. Et ensuite donne-moi le nombre d'habitants, c'est l'ISEE qui va t'y aider. Quand je saurai ce nombre, je pourrai partir en paix".
> 
> Voici le nombre de coquilles d'escargots trouvés pendant plus d'un mois. Ensuite, plus aucun tas...
> 
> 45 50 50 46 48 51 55 53 51 57 54 49 52 52 57 53 48 55 56 44 32 49 54 54 46 50 54 57 55 56 49 57 49 55 48 49 55 57
> 
> Ben longîînnnn me voilà mal barré... Tu peux m'aider à trouver ?
> 
> Le flag est de la forme : OPENNC{nombre_habitants_encodé_en_base_64}
> 
> Nota : Attention, tu as un nombre très limité de soumissions ;)
> 
> Auteur : Kerhuon


## Résolution

on convertie le hex : `https://www.dcode.fr/ascii-code`

ça donne `-22.037539614495078, 166.2697819170179` qui pointe vers **bangou**

On cherche isee et bangou et on tombe sur https://www.isee.nc/component/phocadownload/category/49-paita?download=393:2151bangou

Du coup on récupère les habitant de 2019 : **308** et on converti en b64 `echo -ne '308' | base64`


>[!question]- Spoiler du flag
> OPENNC{MzA4}

