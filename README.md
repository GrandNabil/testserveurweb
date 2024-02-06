# testserveurweb

### Etape 1: Préparation et Endurcissement du Serveur

#### Installation du serveur Linux:
Ici le serveur mis à ma disposition est un serveur ubuntu.

#### Check-list de sécurisation du serveur
- Modification du mot de passe root (changeme) par un mot de passe complexe(258oO#Test)
    Je fais cette modification pour éviter l'utilisation non autorisée du compte super utilisateur.
  
    ![modification de mot de passe](https://github.com/GrandNabil/testserveurweb/assets/99473954/b3650936-2e92-4205-8717-c2171d2a194a)
  
- Désactivation de la connexion SSH par mot de passe.
  Je fais cette désactivation parce que avec la connexion par mot de passe, il y a plus de risque qu'il soit découvert.
  La connexion par clés publiques/privées a été déjà configuré  ici; l'outil utilisé pour le faire est openssl.

  ![Désactivation de la connexion SSH par mot de passe.](https://github.com/GrandNabil/testserveurweb/assets/99473954/006617e3-c31d-49ae-a0f5-9dd5109daac3)


  J'ai modifié le fichier `etc/ssh/sshd_config` pour la désactivation de la connexion par SSH et le changement de port SSH

- Désactivation des ports inutilisés.
  Par défaut, les ports sont ouverts et pour une meilleure sécurité, je ferme les ports qui ne seront pas utilisés ici.
  Pour le faire, j'utilise le pare-feu UFW. UFW parce que c'est simple à utiliser et il permet de créer des règles efficaces.
  Je bloque par défaut les connexions entrantes et j'autorise les connexions sortantes
  Ensuite j'autoirse ssh , https, htpp pour les services web. Je m'en arrête là. S'il y'a dautres règles après elles seront ajoutées.

  
    ![Configuration Pare-feu)](https://github.com/GrandNabil/testserveurweb/assets/99473954/48e71a38-a59b-4159-8ae6-15930ae6ec59)
    ![configuration pare feu](https://github.com/GrandNabil/testserveurweb/assets/99473954/1b95c094-0d71-4a44-8c25-81c273bd48a5)



- Faire la mise à jour des paquets et vérifer qu'ils sont à jours. 

### Etape 2: Mise en Place du Serveur Web Sécurisé

-Avant d'installer le site Wordpress, je vais d'abord installer mon serveur LAMP. Le serveur LAMP c'est un ensemble de composants : le système d'explitation (ici Linux), le serveur web(Apache), le gestionnaire de base de données (MariaDB/MySQL) et le gestionnaire de scripts(PHP).
On commence d'abord par la mise à jour des paquets
Ensuite installation du serveur web Apache2.
    ![mise à jour et installation du serveur apache)](https://github.com/GrandNabil/testserveurweb/assets/99473954/98ca5004-7f08-4fa8-aa9e-7fe200c31d72)

Verification que le serveur est bien installé. 
J'ai lancé la page d'accueil avec l'outil en ligne de commande Lynx qui permet de voir des pages web dans le terminal bien sûr sans le graphique. Pour configurer Wordpress j'utiliserai l'adresse publique du serveur pour accéder à l'interface à partir d'un navigateur distant
![Capture d’écran (157)](https://github.com/GrandNabil/testserveurweb/assets/99473954/eb5c8aad-c55b-48b2-9d64-cd2ddf4f0b91)
![Capture d’écran (156)](https://github.com/GrandNabil/testserveurweb/assets/99473954/843978ee-10ea-4f01-bc65-3b09c2bdf88f) 

Pour des mesures de sécurité, je vérifie la version de apache pour voir si c'est la dernière. La version instalée est la 2.4.52 qui est la dernière.

- Installation de PHP
  PHP va interagir avec le serveur apache et avec la base de données comme une extension afin de pouvoir traiter les scripts intégrés aux pages. Puisque c'est un siteweb wordpress qui doit être installé, php est plus approprié.
    ![Capture d’écran (159)](https://github.com/GrandNabil/testserveurweb/assets/99473954/4a5cb68e-95bd-4101-afd4-ebb0c6c55bd3)
    ![Capture d’écran (161)](https://github.com/GrandNabil/testserveurweb/assets/99473954/db3e4a98-8d8b-491d-af22-1e0d34942a26)
    ![Capture d’écran (162)](https://github.com/GrandNabil/testserveurweb/assets/99473954/6e659246-9eff-46bc-9fd1-efbcc7ba42d7)
    ![Capture d’écran (164)](https://github.com/GrandNabil/testserveurweb/assets/99473954/ce3670b5-0747-43a4-b6bb-29ecb1b325df)

- Installation du gestionnaire de base de données MariadB
  
![Capture d’écran (167)](https://github.com/GrandNabil/testserveurweb/assets/99473954/eab61de8-4311-4e43-9c42-9cdf6cfe1a3c)
![Capture d’écran (166)](https://github.com/GrandNabil/testserveurweb/assets/99473954/a392f875-db1b-4f4d-b5ba-8bdf6118f0fd)


- Installation de Wordpress
  On commence d'abord par une création de la base de données pour wordpress qui va stocker toutes les informations liées à la configuration et au contenu du site web. A la suite, je crée un utilisateur qui est l'administrateur avec tous les privilèges pour opérer sur la base de données.

   ![Capture d’écran (170)](https://github.com/GrandNabil/testserveurweb/assets/99473954/fb69b118-bff2-4ab7-ae90-1367ac033d47)

Nous allons utiliser le site par défaut d'Apache "/var/www/html" pour stocker les données du site WordPress en le remplaçant par le site wordpress.
D'abord je télécharge le fichier zip de wordpress. Ensuite je décompresse avec l'outil Zip. Ensuite je déplace le dossier wordpress dans vers '/var/www/html' et enfin je donne les doitd d'utilidateur au serveur Apache pour préciser que c'est le serveur web. 'sudo chown -R www-data:www-data /var/www/html/'
Vérification ensuite de l'installation
    ![Capture d’écran (171)](https://github.com/GrandNabil/testserveurweb/assets/99473954/cbca250a-ccfe-49f0-8a18-cc31cbcb46e8)
    ![Capture d’écran (172)](https://github.com/GrandNabil/testserveurweb/assets/99473954/9c50c258-fc57-49f4-a819-570ed116351f)
    ![Capture d’écran (173)](https://github.com/GrandNabil/testserveurweb/assets/99473954/1ae66a02-32be-45eb-bf3e-1bf8dae27bcc)

- Configuration de Wordpress

  Pour accéder à Wordpress sur un navigateur j'ai utilisé l'adresse publique du serveur.
  ![Page d'accueil de wordpress de configuration](https://github.com/GrandNabil/testserveurweb/assets/99473954/b02bdc6d-7d21-4352-874a-3bd6204d823e)


  ![Page de bienvenue](https://github.com/GrandNabil/testserveurweb/assets/99473954/01ba89ea-e62a-422e-bb3e-db387cc32cd3)

  ![Details de connexion à la base de données](https://github.com/GrandNabil/testserveurweb/assets/99473954/8b5143dc-0f4a-477f-9655-107216b13674)


  ![Informations pour le sitess wordpress](https://github.com/GrandNabil/testserveurweb/assets/99473954/1b6fdafb-bc6a-437d-b19f-34b1675f5e8b)

  ![Page de succès](https://github.com/GrandNabil/testserveurweb/assets/99473954/6f031238-402e-4b50-8648-3bc212ada66b)

  ![Dashboard wordpress](https://github.com/GrandNabil/testserveurweb/assets/99473954/e86504f0-13a4-4029-a893-18862fd7a71f)

  

  ![modification de sécurité](https://github.com/GrandNabil/testserveurweb/assets/99473954/037237ee-c5ad-4d1e-ab95-f971c848b7c2)

