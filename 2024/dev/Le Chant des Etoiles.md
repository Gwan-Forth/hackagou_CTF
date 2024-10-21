## Enoncé

>Selon une légende, les étoiles n'étaient pas seulement des points lumineux, mais des esprits anciens, maîtres de la lumière et de l'obscurité. Ils communiquaient à travers un code secret que seuls les sages pouvaient comprendre.
>
>Un jour, un jeune héros nommé Wanaké partit à la recherche des secrets des étoiles. Il avait entendu dire que ceux qui parvenaient à déchiffrer le "Chant des Étoiles" pouvaient acquérir une connaissance infinie, leur permettant de lire le destin et de changer le cours des événements. Cependant, le chemin pour déchiffrer ce chant n'était pas simple : il fallait comprendre le langage caché de la lumière et de l'ombre, le code binaire des esprits célestes.
>
>Lorsque Wanaké parvint à un ancien temple perdu dans la montagne, il trouva deux cristaux lumineux, scintillant d'une étrange énergie. Ces cristaux, selon la légende, représentaient la lumière et l'ombre, chacun codé en langage binaire, sur huit éclats. Pour avancer dans sa quête, Wanaké devait répondre aux questions posées par les gardiens des étoiles, des esprits capables de manipuler ces cristaux selon des lois binaires sacrées.
>
>Les gardiens posèrent à Wanaké six questions sur le fonctionnement des cristaux, utilisant leur code sacré pour tester ses connaissances :
>
>1. L’union des esprits : Que se passe-t-il lorsque les cristaux partagent une partie de leur énergie commune (&) ?
>2. Le souffle cosmique : Comment les cristaux se combinent-ils pour libérer toute leur énergie dans une seule explosion lumineuse (|) ?
>3. L’équilibre des mondes : Si deux cristaux fusionnent, quelle sera leur nouvelle force combinée (+) ?
>4. La multiplication des éclats : Que se passe-t-il lorsque l'énergie d'un cristal se multiplie par celle d'un autre (* ) ?
>5. Le déplacement des étoiles : Comment la lumière d’un cristal se déplace-t-elle dans le ciel lorsque le vent céleste souffle vers l’Est (<<) ?
>6. Le voyage des astres : Et comment la lumière d’un cristal recule-t-elle vers l’Ouest lorsque le vent souffle en sens inverse (>>) ?
>
>Wanaké savait que s'il répondait correctement à toutes ces questions, il pourrait comprendre le Chant des Étoiles et accéder à une sagesse ancienne. Les cristaux représentaient des nombres binaires, et chaque opération qu'il devait accomplir n'était autre qu'un test pour maîtriser les interactions des étoiles dans leur langage céleste.

## Résolution

Ici tout est dans le titre, il faut faire un script pour répondre aux différentes questions que l’on va nous poser : 

```python
from pwn import *  
import re  
  
# connexion au serveur  
p = remote('challenges.hackagou.nc', 5009)  

# On boucle sur le nombre de challenge
for challenge_id in range(6):  
	# recupération de l'énoncé et on décode les bytes
    challenge = p.recv().decode()  
    #print(challenge)  
    
    # on recherche l'opération dans le challenge grace à une regex
    # on split le résultat dans des variables
    a, op, b = re.search(r'\d+ [|&^><*+-]* \d+', challenge).group().split(' ')  
    print(a, op, b)  
    # conversion du binaire en int
    a = int(a, 2)  
    # on essaye la conversion binaire -> int
    try:  
        b = int(b, 2)  
    # si ça ne fonctionne pas c'est que ce n'est pas un binaire mais un int tout court
    except:  
        b = int(b)  
    # on execute l'opération pour avoir le résultat
    result = eval(f'{a} {op} {b}')  
    # on transforme le résultat en binaire en rajoutant les leading 0 si besoin pour avoir un binaire sur 8 chiffres et on envoi le résultat
    p.sendline(f'{result:08b}')  

# on a fini tous les challenge du coup on récupère le flag  et on l'affiche
print(p.recv().decode())  
# fermeture de connexion au serveur
p.close()
```



>[!question]- Spoiler du flag
> OPENNC{B1n4rY_1s_F0r_31337_0nLY}

