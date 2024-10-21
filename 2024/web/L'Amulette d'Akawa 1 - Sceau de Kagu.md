## Enoncé

> Dans les temps anciens, au cœur de la Nouvelle-Calédonie, vivait un sorcier nommé Akawa, détenteur d'une amulette aux pouvoirs immenses. Cette amulette pouvait conférer à son porteur la capacité de commander les esprits de la nature, contrôlant ainsi les éléments et les créatures magiques. Mais, pour éviter qu'elle ne tombe entre de mauvaises mains, Akawa l'a enfermée dans une grotte cachée, protégée par des énigmes et des sorts puissants.
> 
> Cependant, une légende raconte que seuls ceux qui sont capables de résoudre les mystères laissés par Akawa peuvent récupérer l'amulette. Tu es l'un des rares à avoir découvert l'entrée de la grotte. Maintenant, il te faut franchir les quatre obstacles qui protègent cet artefact.
> 
> En entrant dans la grotte, tu te retrouves face à un immense oiseau de pierre, le Kagu, une créature emblématique de la forêt calédonienne. Sur son bec est gravée une inscription : "Seuls ceux qui détiennent la vérité peuvent passer."
> 
> Au pied de la statue, une petite boîte de bois est fermée par un sceau magique. Ce sceau contient une simple inscription codée que tu découvres : **YWRtaW49MA\=\=**.
> 
> Ton instinct te dit que ce n'est qu'une barrière illusoire. Si tu arrives à révéler la vérité cachée derrière cet encodage, tu pourras lever ce premier obstacle.

## Résolution

Dans l’énoncé on a cet indice `YWRtaW49MA==`
C’est du base64 et quand on le déchiffre : 
```bash
┌──(kali㉿kali)-[~/hackagou]
└─$ echo 'YWRtaW49MA==' | base64 -d                                
admin=0 
```

On va utilier burpsuite pour suivre l’échange entre nous et le serveur web. Après être arrivé sur le formulaire de connexion et de le soumettre, on remarque que le serveur nous renvoi un cookie : `Cookie: auth=YWRtaW49MA==` qui est exactement celui que l’on a dans l’énoncé.

Si on continu on se retrouve face à une erreur qui nous dit `Seuls ceux qui détiennent la vérité peuvent passer.`

A partir de là on suppose qu’on doit faire en sorte d’être admin au yeux du site et la réponse réside dans le cookie.

Si on part du principe que dans `admin=0` le `0` est un boolean, alors la chaine indique que nous ne somme pas admin. Si on veux l’être il faudrait que la chaine soit `admin=1`.

On va donc chiffrer en base64 cette chaine et remplacer notre cookie. Ce qui nous donne :
```bash
┌──(kali㉿kali)-[~/hackagou]
└─$ echo 'admin=1' | base64
YWRtaW49MQo=
```

Il ne reste plus qu’à mettre cette valeur dans le cookie, contacter le site et on obtient le flag.

>[!question]- Spoiler du flag
> OPENNC{b45364_1s_N07_4_s3cUr17Y!!}

