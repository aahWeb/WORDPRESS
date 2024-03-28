# Télécharger WordPress

Vous pouvez télécharger WordPress sur ce lien : https://wordpress.org/download/

Il vous faudra déziper le fichier `.zip` et mettre les fichiers racine dans le répertoire de projet WordPress.

Ce répertoire est un simple dossier que vous placerez dans le `htdocs/` de XAMPP ou ailleurs selon que vous utilisez XAMPP ou le serveur web de wp-cli (ou autres serveurs web).

# Installation avec XAMPP

Premièrement nous allons télécharger XAMPP et exécuter l'installer : https://www.apachefriends.org/fr/download.html

Ensuite rendez-vous dans le répertoire `htdocs\`, là où l'on met nos applications. (Vous pouvez accéder à ce dossier depuis le dashboard de XAMPP)

Vous pouvez créer un répertoire dans lequel on déposera les fichiers racine de notre application WordPress.

# Installation avec WP-CLI

WP-CLI est un outil qui nous permet d'interagir avec WordPress via des lignes de commande.

On a le choix entre deux types d'installation, soit de manière globale (dans les variables d'environnement), soit de manière locale à un répertoire.

Pour télécharger WP-CLI, exécutez la commande :

```shell
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
```

Pour ceux qui n'ont pas `curl` vous pouvez télécharger manuellement le `.phar` : https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar

Renomez ce fichier `wp-cli.phar` en `wp.phar`, ce sera plus commode pour la suite.

## installation local à l'application WordPress

Vous avez juste à placer le `wp.phar` dans le répertoire de l'application.

Pour exécuter une commande wp-cli, vous avez juste à faire `php ./wp.phar`. Par exemple exécuter cette commande :

```shell
php ./wp.phar --info
```

## Utilisateurs macOS, installation global

Premièrement sur système UNIX (macOS inclue) vous pouvez changer les permissions du `wp.phar` :

```bash
chmod +x wp.phar
```

et l'ajouter dans vos variables d'environnement :

```bash
mv ./wp.phar /usr/local/bin/
```

Si l'installation ses bien passé, vous devriez pouvoir exécuter la commande `wp --info`

## Utilisateurs Windows, installation global

Pour une installation globale sur un système Windows, il faudra d'abord choisir dans quel dossier se trouvera wp-cli.

Prenez par exemple la racine de votre système `C://`, créez-y un dossier `wp-cli/`, dans lequel vous placerez le fichier téléchargé `wp.phar`. Et en fonction que vous soyez sur le cmd.exe ou PowerShell, exécuté la commande adaptée :
- cmd.exe : `echo @php "%~dp0wp.phar" %*>wp.bat`
- PowerShell : `Set-Content wp.bat '@php "%~dp0wp.phar" %*'`

Vous venez de créer un fichier exécutable `.bat` que vous pouvez renseigner dans vos varibles d'environnement.

Il faut renseigner le dossier dans lequel se trouve votre fichier `.bat`.

Dans notre exemple, ça donne : `C://wp-cli`

Si l'installation ses bien passé, vous devriez pouvoir exécuter la commande `wp --info`

# Lancer notre application WordPress sur un serveur local

## Lancer un serveur web avec XAMPP

Depuis l'interface de XAMPP, allé dans l'onglet "Manage servers", lancez le serveur Apache et la base de données MySQL.

> [!NOTE]
> Si votre base de données MySQL ne se lance pas, c'est peut-être qu'une autre base de données occupe le port. Il vous faut arrêter cette base de données pour ensuite lancer celle de XAMPP.
>
> Sur Windows :  
> Entrez le raccourcie **CTRL + R**, tapez "**services.msc**". Cherchez le service qui correspondrait à une base de données et arrêtez-la.
>
> Sur macOS (Homebrew) :  
> Dans la console tapez `brew services list`, vous devriez retrouver une liste des services qui tournent et qui sont gérés par homebrew. Tapez `brew services stop nom_du_service` (si vous trouvez MySQL : `brew services stop mysql`).

## Lancer un serveur web avec wp-cli

wp-cli embarque un serveur web légé, en réalité c'est le serveur web de PHP mais configuré pour faire tourner wordpress.

Depuis votre terminale, placez-vous à la racine de votre application WordPress. Vous pouvez maintenant lancer la commande `wp server` et le tour est joué !

# L'installation en 5 min de WordPress

WordPress va d'abord vous demander l'accès à une base de données. Il faut créer cette base de données pour continuer.

## Le serveur MySQL dans XAMPP

Pour créer une base de données dans XAMPP, il faut déjà trouver le fichier binaire mysql.

Et depuis le répertoire où se trouve ce fichier (en général dans un répertoire `bin/`) créé une base de données via la commande suivante :

```shell
./mysql -uroot -e 'CREATE DATABASE nom_de_votre_bdd;'
```

## En utilisant un serveur MySQL externe à XAMPP

Si le dossier bin de MySQL est défini dans vos variables d'environnement, vous n'avez qu'à exécuter la commande :

```shell
mysql -uroot -e 'CREATE DATABASE wp_portfolio_photo;'
```


> [!WARNING]
> Si votre base de données MySQL est protégée par un mot de passe, ajouter l'option -p. À la connexion, MySQL vous demandera d'entrer le mot de passe.