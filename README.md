# Création du Docker pour un projet Symfony 6

D'après les travaux de :
- le tutoriel de [Yoan Dev](https://yoandev.co/un-environnement-de-developpement-symfony-5-avec-docker-et-docker-compose) 
- le .git de [arkste](https://github.com/arkste/docker-symfony)
- le .git de [deluan](https://github.com/deluan/zsh-in-docker) 

## Contenu du Docker
- PHP 8.1
- Apache
- Maildev
- MariaDB
- phpMyAdmin
- Node
- Yarn
- Zsh

## Comment ça marche ?
C'est une très bonne question !
Bien que fonctionnel, ce docker n'en est pas moins expérimental et j'espère le faire évoluer régulièrement.
### Comment l'utiliser alors ?
A vrai dire, un simple : `docker-compose up -d` permet de créer les images nécessaires.
Je vous invite cependant à modifier le `.env`
J'utilise personnellement mon nom d'utilisateur / groupe WSL (`fanouu`) dans les variables `USER` et `GROUP`

D'autres variables sont également disponibles :
- `PHP_APACHE_PORT`, `PHPMYADMIN_PORT`, `MAILDEV_PORT`, Qui permettent de configurer le port des services indiqués 
- `SYMFONY_FOLDER_NAME` qui est le répertoire de votre projet web. 
- `PROJECT_NAME` que j'utilise pour renommer les images docker
> Si vous souhaitez modifier le nom du répertoire de votre projet, renommez le dossier `/symfony` , modifiez la variable `SYMFONY_FOLDER_NAME` dans `.env`  et le nom de dossier dans le `.gitignore`

## Démarrons !
J'ai souhaité avoir un fichier docker que j'utiliserai dans mes différents projets.
Toutefois, je souhaite séparer mes projets de ma configuration docker. 
Je m'y prends donc ainsi : 
- `git clone git@github.com:Fan0u/docker-symfony6.git`
- `mv docker-symfony6 nom_de_mon_dossier`
- `cd nom_de_mon_dossier` 
- `mkdir SYMFONY_FOLDER_NAME` ⚠ Ce dossier doit porter le même nom que celui défini dans `SYMFONY_FOLDER_NAME` du fichier `.env` 
- `docker-compose up -d` ... et j'attends que la machine fasse son job :)
- `docker ps` pour avoir les ID de nos containers 
- `docker exec -it ID_DU_CONTAINER_DONT_LE_NOM_EST_php_apache_nom_du_projet bash` (n'oubliez pas le bash)
    - exemple : `docker exec -it 2ebadf41d749 bash`     

Puis dans le bash de notre docker container, je lance la commande pour créer un projet symfony
- `symfony console new .`

edit