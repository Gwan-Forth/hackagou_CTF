Il semblerait que deux perroquets, Dé et Ness, aient communiqué de manière à ne pas se faire repérer depuis la planque du pirate qui s'amuse à cacher des trésors. ![deetness-400x400.png](https://ctf2023.hackagou.nc/files/30a843913e22f16313f5da7550f55454/deetness-400x400.png) 
Saurez-vous déchiffrer le contenu de leur conversation ?

![deetness](../../../../attachements/deetness.pcapng)

## Résolution

Ici on a droit à un fichier pcap qui contient un échange entre un client et un serveur DNS.
```pcap
1	0.000000000	172.18.0.1	172.18.0.2	DNS	65	Standard query 0x1234 A T.com
2	0.000086733	172.18.0.2	172.18.0.1	DNS	65	Standard query response 0x5678 A 1.com[Malformed Packet]
3	0.000112061	172.18.0.1	172.18.0.2	DNS	65	Standard query 0x1234 A B.com
4	0.000123341	172.18.0.2	172.18.0.1	DNS	65	Standard query response 0x5678 A F.com[Malformed Packet]
```

On peux voir que les requêtes et les réponses sont différentes :
- T.com
- 1.com
- B.com
- F.com

Si on enlève le domaine **.com** on se retrouve avec ***T1BF*** pour les 4 première requêtes. Il suffit de poursuivre le même procédé avec le reste du fichier.

A faire à la main ou alors en utilisant [tshark](../../../../ressouces/scripts/tshark.md) 

On part donc du principe qu’il faut extraire chaque 

>[!question]- Spoiler du flag
> OPENNC{}

