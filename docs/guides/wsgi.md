# WSGI, une introduction

## Pourquoi WSGI est nécessaire ?

### Le problème de la portabilité

Avant l'arrivée de WSGI, le monde du développement web en Python était un peu
comme le Far West. Chaque framework web avait son propre moyen de communiquer
avec les serveurs web, et vice versa. Cela signifiait que si tu développais une
application en utilisant un certain framework, tu étais souvent lié à un
serveur web spécifique. Changer de serveur web ou de framework pouvait être un
véritable casse-tête, nécessitant des ajustements majeurs dans le code.

### Un besoin d'uniformité

Le manque d'un standard commun rendait également difficile la réutilisation du
code et des composants entre différents projets et frameworks. Par exemple, si
tu avais un morceau de middleware très utile dans un projet Django, il était
difficile de le transférer dans un projet Flask sans modifications importantes.


### La solution : WSGI

C'est là qu'intervient WSGI (Web Server Gateway Interface). WSGI agit comme un
intermédiaire entre le serveur web et l'application web, permettant une
communication fluide entre les deux, quel que soit le serveur web ou le
framework utilisé. En d'autres termes, WSGI est un contrat qui dit : "Si tu
suis ces règles, ton application web pourra communiquer avec n'importe quel
serveur web qui suit également ces règles, et vice versa."

### Les avantages

1. **Portabilité** : Tu peux facilement passer d'un serveur web à un autre sans
   avoir à réécrire ton application.
2. **Réutilisabilité** : Les composants, comme les middlewares, peuvent être
   réutilisés entre différents projets et frameworks.
3. **Flexibilité** : Tu as la liberté de choisir le serveur web et le framework
   qui correspondent le mieux à tes besoins, sans être enfermé dans un
   écosystème particulier.

En résumé, WSGI apporte une standardisation bien nécessaire à l'écosystème
Python pour le développement web, rendant la vie beaucoup plus facile pour
nous, les développeurs.

## Terminologie

### Interface WSGI

L'**interface WSGI** a deux parties: la partie *serveur* ou *gateway* et la
partie *application* ou *framework*. La partie *serveur* appelle un objet
*callable* (généralement une fonction) qui est la partie *application*.

### Application WSGI

Une **application WSGI** est un programme Python qui se conforme à la
spécification WSGI. Elle prend en charge deux arguments : un dictionnaire
d'environnement (`environ`) et une fonction de démarrage de réponse
(`start_response`). L'application renvoie un itérable pour le corps de la réponse
HTTP.

### Serveur WSGI

Un **serveur WSGI** est un serveur web qui sait comment interagir avec une
application WSGI. Il passe les informations de la requête HTTP à l'application
via le dictionnaire `environ` et reçoit les détails de la réponse via
`start_response`.

### Middleware WSGI

Un **middleware WSGI** est un composant qui se situe entre le serveur WSGI et
l'application WSGI. Il peut modifier la requête ou la réponse, ou même décider
de ne pas appeler l'application du tout. On peut enchaîner plusieurs
middlewares les uns à la suite des autres.

### `environ`

C'est un dictionnaire Python qui contient toutes les variables d'environnement
HTTP. Il est passé de votre serveur WSGI à votre application WSGI.

### `start_response`

C'est fonction callback que le serveur WSGI passe à l'application WSGI.
L'application l'appelle pour définir les en-têtes de la réponse HTTP et le code
de statut.

### Réponse itérable

L'application WSGI doit renvoyer un itérable pour le corps de la réponse HTTP.
Le serveur WSGI itère sur cet itérable pour obtenir les données de la réponse.

--WIP--



