
> La légende de Poena'iki est emplie de mystères. Nul ne sait exactement où sa mère s'est transformée en être magique.
> 
> Le descendant d'un ancien tahu’a, qui possède un secret de famille, a bien voulu révéler le lieu mystique. Mais il tient à demeurer anonyme et nous a déclaré qu'il enverrait un message secret sur notre serveur Web.
> 
> Aide-nous à trouver ce lieu !
> 
> Le flag est de la forme : OPENNC{quelque_chose}
> 
> Auteur : Kerhuon

![logs](logs.txt)
## Résolution

On analyse le fichier de logs et on trouve qu’il y a des requêtes intéressantes du genre : 
`202.22.123.20 - - [30/Sep/2024:12:06:01 +0000] "POST /home HTTP/1.1" 200 512 "https://ctf.hackagou.nc/dashboard" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.164 Safari/537.36" "data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%28118%29%2C15%29%7C%7C"`

La partie qui va probablement nous intéresser le plus : `data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%28118%29%2C15%29%7C%7C`

Si on récupère des données dans toutes les logs on se retrouve avec : 
```
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%28118%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%28111%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%28105%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2899%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%28105%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2832%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%28108%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%28101%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2832%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%28102%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%28108%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2897%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%28103%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2832%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2858%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2832%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2879%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2880%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2869%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2878%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2878%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2867%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%28123%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2865%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%28110%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2897%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%28104%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%2848%29%2C15%29%7C%7C"
data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%28125%29%2C15%29%7C%7C"
```

On remarque qu’il y a beaucoup de choses qui se répète et dont on n’a donc probablement pas besoin :
* prefix : `data%3D%7CDBMS_PIPE.RECEIVE_MESSAGE%28CHR%28`
* suffixe : `%29%2C15%29%7C%7C`

Une fois qu’on à retiré tout ça il nous reste : 
```
118
111
105
99
105
32
108
101
32
102
108
97
103
32
58
32
79
80
69
78
78
67
123
65
110
97
104
48
125
```

On envoi ça dans [cyberchef](../../../../ressouces/tools/cyberchef.md) et il nous propose magiquement la recette `From Decimal` et on a notre flag.

>[!question]- Spoiler du flag
> OPENNC{Anah0}

