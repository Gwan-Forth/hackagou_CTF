> Dans un passé lointain, bien avant que les navigateurs modernes ne cartographient les vastes océans, il y avait un peuple ancien et puissant connu sous le nom des Orihena. Ils étaient réputés pour leur sagesse et leur connexion profonde avec l'océan, dominant les eaux et maîtrisant les secrets de la navigation.
> 
> Cependant, leur existence prospère a été brutalement interrompue par l'arrivée des Maruhana, un peuple rival cherchant à s'étendre. Les Maruhana ont conquis les Orihena et, dans leur soif de pouvoir, ont réécrit l'histoire, effaçant lentement les traces de la grandeur des Orihena. Au fil du temps, les récits de leurs exploits ont été transformés, modifiés et parfois complètement effacés, laissant derrière eux une version altérée de la vérité.
> 
> Pourtant, quelque part, au fond d'un vieux manuscrit perdu, la vraie histoire des Orihena subsiste... et c'est à vous de la retrouver.
> 
> Vous avez été chargé de retrouver la véritable histoire des Orihena avant que les Maruhana ne la détruisent complètement. Vous avez en votre possession un de ces passages historiques.
> 
> Format du flag : OPENNC{quelque_chose}
> 
> Auteur : Ketsui


![Histoire_modifiee.tar](../../../../attachements/Histoire_modifiee.tar.gz)


## Résolution

on récupère le tar.gz et on décompresse.

On regarde l’historique de git : `git log`
```
┌──(kali㉿kali)-[/mnt/forensics/histoire/Histoire_modifiee]
└─$ sudo git log 
commit 368f555333c663e7a61bb11940056ac08133351a (HEAD -> master)
Author: Tchia <Tchia@awaceb.com>
Date:   Sat Aug 24 09:49:16 2024 +1100

    Réécriture complète du récit par les Maruhana.

commit 97ffc818cc068ebb02ccf00c58894e7bfb5456cf
Author: Tchia <Tchia@awaceb.com>
Date:   Sat Aug 24 09:48:39 2024 +1100

    modification

commit 9e6f9eff97d2773a4ac9621b04bceed92c769e15
Author: Tchia <Tchia@awaceb.com>
Date:   Sat Aug 24 09:47:47 2024 +1100

    Récit initial
```

On veux récupérer le récit initial donc : `git checkout 9e6f9eff97d2773a4ac9621b04bceed92c769e15`

Il ne reste plus qu’à ouvrit le fichier et récupérer le flag dedans.

>[!question]- Spoiler du flag
> OPENNC{La_Vraie_Histoire}

