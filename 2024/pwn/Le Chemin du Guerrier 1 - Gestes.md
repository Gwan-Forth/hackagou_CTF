## Enoncé

>Sur l'île mystique de Naori, où les légendes prennent vie, chaque guerrier aspirant doit d'abord prouver qu'il est digne d'accéder aux secrets des anciens. La première étape du Chemin du Guerrier est d'une simplicité trompeuse, mais elle est essentielle pour établir une connexion avec les esprits guerriers qui habitent ces terres sacrées.
>
>Dans les contes des anciens, on raconte que les premiers guerriers de Naori communiquaient avec les esprits et invoquaient leur puissance à travers une série de gestes précis et rituels. Ces gestes, aussi simples qu'ils puissent paraître, sont la base de toute interaction avec les forces invisibles de l'île. Le moindre faux mouvement peut mettre fin à l'initiation d'un aspirant.
>
>Vous êtes maintenant face à votre première épreuve : "Les Gestes Ancestraux". À l'entrée de la forêt sacrée de Naori, un ancien gardien apparaît sous la forme d'un mystérieux esprit. Cet esprit ne parle pas, mais il observe attentivement chaque mouvement que vous faites.
>
>Pour entrer dans le sanctuaire du guerrier et poursuivre votre quête, vous devez d'abord exécuter correctement une série de gestes rituels. Mais ces gestes ne sont pas simplement des mouvements physiques : ils symbolisent votre capacité à vous connecter aux Totems que vous rencontrerez plus tard.

![[gestes](gestes)

![gestes 1](gestes%201.c)
## Résolution

```c
#include <stdio.h>
#include <stdlib.h>

void init(){
  fclose(stderr);
  setvbuf(stdin,  0, 2, 0);
  setvbuf(stdout, 0, 2, 0);
}

int main() {
  init();
  puts("L'esprit attend...\n\nQuel geste souhaitez-vous faire ?");
  system("/bin/sh");
  return EXIT_SUCCESS;
}
```

Le code est extrêmement simple et il n’y a rien de particulier. En gros le binaire vous fourni une console shell.

Il ne reste donc qu’à lancer la commande netcat : `nc challenges.hackagou.nc 5000`
et récupérer le flag : 
```bash
Quel geste souhaitez-vous faire ?
ls
flag.txt
run
cat flag.txt
```

>[!question]- Spoiler du flag
> OPENNC{L3_Gu3RR13r_b0ug3_37_53_m3U7!!}

