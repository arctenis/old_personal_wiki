# Hello World

Ceci est un guide destiné aux développeurs pour avoir un rapide aperçu du
langage Go.


## Installation

Pour installer Go sur votre machine :

**Linux**

Utiliser le gestionnaire de paquets de votre distribution.

```bash
sudo apt-get install golang
```

ou

```bash
sudo pacman -S go
```

par exemple.

Ou suivre les instructions du site officiel.

1. Télécharger l'archive sur le site officiel.
2. Supprimer l'installation précédente si besoin.
```bash
sudo rm -rf /usr/local/go
```
3. Extraire l'archive dans /usr/local
```bash
sudo tar -C /usr/local -xzf go1.21.0.linux-amd64.tar.gz
```
4. Ajouter /usr/local/go/bin à la variable d'environnement PATH
```bash
export PATH=$PATH:/usr/local/go/bin
```
5. Vérifier que l'installation est fonctionnelle
```bash
go version
```

**MacOS**

1. Ouvrir le fichier .pkg téléchargé.
2. Suivre les instructions.
3. Redémarrer le terminal si besoin.
4. Vérifier que l'installation est fonctionnelle
```bash
go version
```

**Windows**

1. Ouvrir le fichier .msi téléchargé.
2. Suivre les instructions.
3. Lancez l'invite de commande.
4. Vérifier que l'installation est fonctionnelle
```bash
go version
```

## L'outil Go en ligne de commande

Il est utilisé pour diverses tâches, allant de la gestion des dépendances au
build et à l'exécution de vos programmes. Pour commencer, vous pouvez créer un
projet Go en utilisant la commande `go mod init` suivie du nom de votre module.
Cette commande crée un fichier go.mod qui enregistre vos dépendances. Vous
pouvez ensuite utiliser `go build` pour compiler votre code source en
exécutable. Utilisez go run pour exécuter immédiatement un fichier source sans
compilation préalable. L'outil go offre également des fonctionnalités pour
tester votre code avec `go test`, formater votre code avec `go fmt`, et plus
encore. Vous pouvez lister toutes les commandes disponibles avec `go help`.

Pour créer un projet Go et activer le suivi des dépendances pour votre code,
utilisez la commande `go mod init`. Vous créerez ainsi un fichier go.mod , en
spécifiant le nom du module de votre code, connu sous le nom de chemin de
module. Ce fichier aide à gérer les dépendances et est généralement basé sur
l'emplacement de votre dépôt de code source. Si vous prévoyez de partager votre
module, le chemin du module doit être un emplacement valide à partir duquel les
outils Go peuvent le récupérer.

Vous pouvez utiliser un chemin de dépôt Github, par exemple
`votre_compte_github/votre_projet`.

Pour ce guide, nous allons utiliser `example/hello`.

```bash
mkdir hello
cd hello
go mod init example/hello
```

Créez un fichier `hello.go` avec le contenu suivant :

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, world.")
}
```

Exécutez le programme avec la commande `go run` :

```bash
go run hello.go
```

## Hello World


Dans le répertoire précédemment créé, créez un autre fichier `hello.go` avec le
contenu suivant :

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, world.")
}
```

Compilez et éxécutez le programme avec la commande `go run` :

```bash
go run hello.go
```


