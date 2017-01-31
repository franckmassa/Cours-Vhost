#Cours Apache
##Création d'un Vhost
Dans ce cours nous allons voir comment créer un Vhost sur notre propre machine. Le nom du projet et du Vhost sera **monProjet**.  
Toutes les commandes seront à faire dans le terminal.


##Création du dossier de travail
Nous allons créer un dossier pour le projet dans un dossier **www** qui se trouvera dans notre dossier utilisateur (*par ex : /home/mickael/www*).
**Rappel :** L'alias ~ correspond au dossier utilisateur.


    mkdir ~/www/monProjet


##Création du Vhost
Pour la création du Vhost, il faut configurer Apache. Toutes les commandes suivantes seront à faire en super utilisateur.


        sudo -s
Ensuite on va se rendre dans le dossier des Vhost d'Apache :


        cd /etc/apache2/sites-available/
Nous allons maintenant créer un nouveau fichier de configuration avec l'éditeur Nano :
        nano monProjet.conf
Dans Nano coller ce code :


        <VirtualHost *:80>
          ServerAdmin webmaster@monProjet
          ServerName www.monProjet
          ServerAlias monProjet
          DocumentRoot /home/nom_utilisateur/www/monProjet
          <Directory /home/nom_utilisateur/www/monProjet/>
            AllowOverride All
            Require all granted
          </Directory>
          ErrorLog /var/log/apache2/monProjet-error.log
          LogLevel warn
          CustomLog  /var/log/apache2/monProjet-access.log combined
          ServerSignature Off
        </VirtualHost>

**Important :** Pensez bien à modifier **nom_utilisateur** par votre nom d'utilisateur. Cette configuration est minimal. Elle n'est pas à reproduire en production.  
Sauvegardez puis activez ce nouveau Vhost :


        a2ensite monProjet.conf
Relancez la configuration d'Apache :


        service apache2 reload


##Configuration du fichier hosts
Le Vhost étant créé, il faut maintenant dire à notre ordinateur que http://monProjet dirige vers notre machine et pas sur le web. Pour ce faire il faut éditer le fichier hosts.


        cd /etc
        nano hosts


Après la ligne qui commence par 127.0.1.1 ajoutez :


        127.0.0.1 monProjet


##Conclusion
A partir de là vous pouvez afficher la page dans **Firefox** avec l'adresse : http://monProjet
