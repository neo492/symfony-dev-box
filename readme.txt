À lire pour installer la vagrant du projet Alumni CLCF :

	Requirements for vagrant
		- VirtualBox : https://www.virtualbox.org/ 
		- Vagrant : https://www.vagrantup.com/
		- ssh 

		sur windows je vous conseil cmder qui est un emulateur de terminal très pratique et qui integre notament ssh et d'autre commandes manquantes sur windows.
		http://gooseberrycreative.com/cmder/

Installation :

1 - Creer un dossiser 'alumniclcf' à la racine du dossier de la vagrant (Déja fait :) )

2 - Aller dans ce dossier "alumniclcf" 

3 - Cloner le repos alumni avec le projet de base (symfony) : ne pas oublier le point à la fin de la 	 comande !!! : 
	"git clone git@github.com:ecolehetic/alumniCLCF.git ." (sans les "" mais avec le point apres git c'est important !)

4 - executer la commande : "vagrant up"
		le vagrant up va mettre du temps, car il récupere l'image ubuntu et configure la machine virtuel de dev. 
5 - puis "vagrant ssh" : Permet de ce connecter en ssh à la nouvelle machine virtuel grace à vagrant


6 - executer la comande dans la vagrant : "cd /vagrant/alumni" : pour ce déplacer dans le dossier .

7 - Puis la commande : "composer update" ;
	
	Lors du composer update les "vendors" qui sont les composants de symfony sont télécharger ou mis à jours (ils ne sont pas commit sur le repos, c'est inutile car ce sont des composants de symfony)
	
	Il faut ensuite configurer quelques paramètres qui sont demander (cela correspond au fichier /app/config/parameters.yml) 
	
	Il faut garder les parametres par défaut sauf pour, database_name, database_user,database_password  si ce n'est pas déja "alumni" et ainsi que la local à metre en fr et d'ajouter une chaine aléatoire pour "secret"

	voici la configuration qu'il faut : 
	 database_driver: pdo_mysql
	    database_host: 127.0.0.1
	    database_port: null
	    database_name:     alumni
	    database_user:     alumni
	    database_password: alumni
	    mailer_transport: smtp
	    mailer_host: 127.0.0.1
	    mailer_user: null
	    mailer_password: null
	    locale: fr
	    secret: AddRandomSecretPass
	    sass.bin: /usr/local/bin/sass
	    compass.bin: /usr/bin/compass

8 - En suite vous pouvez lancer le server interne de symfony qui peut être utilisé en dev.
	avec la commande suivante :
	"php app/console server:start 0.0.0.0:8000"

	le site est ensuite accesible avec l'ip de la machine vagrant qui est : 192.168.56.127 avec le port 8000

	http://192.168.56.127:8000

	si vous avez une erreur :
	No route found for "GET /"
	404 Not Found - NotFoundHttpException
	C'est tout à fait normal le projet est vraiment vide il n'y a rien pour le moment...
	
9 - Pour voir si cela marche bien : http://192.168.56.127:8000/hello/itsWorks
	il yaura ecrit sans aucun style 'Hello itsWorks' 

10 - Je vous conseil d'ajouter à votre host de votre machine physique 
	 qui est linux ici : /etc/hosts
	 et sur windows ici : C\windows\system32\driver\etc 

	192.168.56.127 alumniclcf.dev
	ps : (le fichier host doit être editer en sudo ou administrateur)

	Ce qui vous permetera d'acceder plus simplement au site 
	http://alumniclcf.dev:8000/

	Quelques explications :
	
	La machine virtuel est une ubuntu 14.04 avec php 5.6 et mysql 5.6 
vagrant permet de faire abstraction de cette machine virtuel et de virtualbox
le principe est de d'avoir un dossier "vagrant-alumni" ou ce trouve cette machine virtuel
dedans ce trouve un dossier partagé "alumniclcf" c'est dans ce dossier depuis votre machine physique que vous allez dev. 
ce dossier etant partager avec la vagrant c'est donc elle qui va jouer le role de serveur !
Donc pour résumer :
Tout ce qui est developpement ces dans le dossier vagrant-alumni/alumniclcf depuis la machine physique
Toute commande symfony ou en rapport avec l'environement de dev est à executer dans la vagrant qu'on accede en ssh après avoir fait un vagrant ssh .


Commande vagrant utile :
	(commande à faire dans le dossier "vagrant-alumni")

Vagrant up : démarer la vm vagrant
vagrant ssh : se connecter à la vm (il faut faire un vagrant up avant)
vagrant halt : eteint la vm
vagrant provision : /!\ permet de metre à jour si il y'a changement de configuration. Ne pas utilisé !

Le dossier vagrant-alumni est composer d'un VagrantFile et du dossier puphpet qui sont la configuration de la vm : ne pas supprimer !

