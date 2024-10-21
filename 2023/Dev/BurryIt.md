
Le second du capitaine aurait, suite à une consommation excessive de breuvages en tout genre, glissé à l'une de ses conquêtes qu'un trésor serait enterré sur une plage de la côte Est.

![buryit-400x400.png](https://ctf2023.hackagou.nc/files/03b230e9c92dd0ff0434b47835f27c4e/buryit-400x400.png) 
Armez-vous d'une pelle pour le retrouver.

![buryit](../../../../attachements/buryit)

## Résolution

Il faut étudier le fichier pour savoir de quoi il s’agit : 

```bash
$ file buryit
buryit: gzip compressed data, last modified: Wed Nov 30 10:21:40 2022, max compression, original size modulo 2^32 81178
```

On peux donc voir qu’il s’agit d’une archive compressé en gzip.

On essaye de le décompresser, pour ça on doit d’abord lui donner une extension pour que le fichier soit traitable par la commande de décompression :
```bash
$ mv buryit buryit.gz
$ gunzip buryit.gz
```

Et tada, on se retrouve à nouveau avec un fichier buryit. Est-ce que c’est le même ?
```bash
$ file buryit
buryit: gzip compressed data, last modified: Wed Nov 30 10:21:40 2022, max compression, original size modulo 2^32 81296
```

On pourrait croire que oui, mais si on regarde de plus près on voit que le modulo n’est pas le même.
Et si on recommence la décompression comme on l’a fait précédemment : 
```bash
$ file buryit
buryit: XZ compressed data, checksum CRC64
```

A partir de là, on comprend qu’un fichier à été compressé telle des poupées russes, mais surtout on peux partir du fait que ça à été fait avec plusieurs types d’archives pour complexifier la chose.

On peux continuer à la main mais on ne saura pas combien de temps ça va prendre ou on peux scripter tout ça. C’est ce qu’on doit faire au vu de la catégorie **dev**.

C’est donc partit pour un script qui va s’occuper de ça : 
![archive recursive](../../../../ressouces/scripts/archive%20recursive.md)

>[!tip]- Sans script bon courage
> Pour information, il y a une imbrication de 2001 archives.

>[!question]- Spoiler du flag
> OPENNC{D4n5_L4_C4P174L3}

