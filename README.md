### testserveurweb

## Etape 1: Préparation et Endurcissement du Serveur

### Installation du serveur Linux:
Ici le serveur mis à ma disposition est un serveur Ubuntu.

### Check-list de sécurisation du serveur
- Modification du mot de passe root par un mot de passe complexe (258oO#Test)
  Je fais cette modification pour éviter l'utilisation non autorisée du compte super utilisateur.
  
  ![modification de mot de passe](https://github.com/GrandNabil/testserveurweb/assets/99473954/b3650936-2e92-4205-8717-c2171d2a194a)
  
- Désactivation de la connexion SSH par mot de passe.
  Je fais cette désactivation parce que la connexion par mot de passe présente un risque plus élevé d'être découvert. La connexion par clés publiques/privées a été déjà configurée ici ; l'outil utilisé pour le faire est OpenSSL.

  ![Désactivation de la connexion SSH par mot de passe](https://github.com/GrandNabil/testserveurweb/assets/99473954/006617e3-c31d-49ae-a0f5-9dd5109daac3)

  J'ai modifié le fichier `etc/ssh/sshd_config` pour la désactivation de la connexion par SSH et le changement de port SSH.

- Désactivation des ports inutilisés.
  Par défaut, les ports sont ouverts et pour une meilleure sécurité, je ferme les ports qui ne seront pas utilisés ici. Pour le faire, j'utilise le pare-feu UFW. UFW parce que c'est simple à utiliser et il permet de créer des règles efficaces. Je bloque par défaut les connexions entrantes et j'autorise les connexions sortantes. Ensuite, j'autorise SSH, HTTPS, HTTP pour les services web. Je m'arrête là. S'il y a d'autres règles après elles seront ajoutées.

  ![configuration pare-feu](https://github.com/GrandNabil/testserveurweb/assets/99473954/0d7ecef4-a846-41b3-847f-003c3d4b0035)
  ![configuration pare-feu](https://github.com/GrandNabil/testserveurweb/assets/99473954/1b95c094-0d71-4a44-8c25-81c273bd48a5)

- Mise à jour des paquets et vérification qu'ils sont à jour.

## Etape 2: Mise en Place du Serveur Web Sécurisé

- Avant d'installer le site Wordpress, je vais d'abord installer un serveur LAMP. Le serveur LAMP est un ensemble de composants : le système d'exploitation (ici Linux), le serveur web (Apache), le gestionnaire de base de données (MariaDB/MySQL) et le gestionnaire de scripts (PHP).
  On commence d'abord par la mise à jour des paquets. Ensuite, installation du serveur web Apache2.

  ![mise à jour et installation du serveur Apache](https://github.com/GrandNabil/testserveurweb/assets/99473954/98ca5004-7f08-4fa8-aa9e-7fe200c31d72)

  Vérification que le serveur est bien installé. J'ai lancé la page d'accueil avec l'outil en ligne de commande Lynx qui permet de voir des pages web dans le terminal bien sûr sans le graphique. Pour configurer Wordpress j'utiliserai l'adresse publique du serveur pour accéder à l'interface à partir d'un navigateur distant.

  ![page d'accueil Apache](https://github.com/GrandNabil/testserveurweb/assets/99473954/eb5c8aad-c55b-48b2-9d64-cd2ddf4f0b91)
  ![page d'accueil Apache](https://github.com/GrandNabil/testserveurweb/assets/99473954/843978ee-10ea-4f01-bc65-3b09c2bdf88f) 

  Pour des mesures de sécurité, je vérifie la version d'Apache pour voir si c'est la dernière. La version installée est la 2.4.52 qui est la dernière.

  Pour continuer avec la sécurité du serveur web, je configure 'a2enmod ssl' pour gérer les certificats SSL et donc l'utilisation du protocole HTTPS
      ![ssl](https://github.com/GrandNabil/testserveurweb/assets/99473954/ee98a2ec-ce25-41c5-b152-b7df9c62637f)


  Restriction de l'accès aux fichiers du serveur en spécifiant des règles de configuration qui permettent de contrôler finement l'accès aux fichiers et répertoires sur le serveur. Ici je restreins les requêtes d'accès à '/var/www/html/restricted' et '/var/www/' il est donc impossible aux utilisateurs d'accéder aux fichiers ou répertoires à l'intérieur de ce répertoire
  
    ![Capture d’écran (189)](https://github.com/GrandNabil/testserveurweb/assets/99473954/487c15b7-0188-4f24-98e5-1fda44ce7446)

Dernière configuration de base de sécurité; j'installe ModSecurity. C' est un pare feu qui s'intègre directement au serveur apache. Contrairement au pare-feu UFW qui est pour tout le serveur.


![Capture d’écran (190)](https://github.com/GrandNabil/testserveurweb/assets/99473954/b15947e7-434c-4242-bf5d-2cabb86d48b9)

      


- Installation de PHP
  PHP va interagir avec le serveur Apache et avec la base de données comme une extension afin de pouvoir traiter les scripts intégrés aux pages. Puisque c'est un site web WordPress qui doit être installé, PHP est plus approprié.

  ![Version PHP](https://github.com/GrandNabil/testserveurweb/assets/99473954/4a5cb68e-95bd-4101-afd4-ebb0c6c55bd3)

  Installation de paquets supplémentaires pour compléter l'installation de PHP pour permettre les interactions entre PHP et notre instance MariaDB.

  ![Installation de paquets](https://github.com/GrandNabil/testserveurweb/assets/99473954/db3e4a98-8d8b-491d-af22-1e0d34942a26)
  
  On vérifie que le moteur de script PHP est bien actif avec la création du fichier "phpinfo.php" à la racine de notre site Web.

  ![script PHP](https://github.com/GrandNabil/testserveurweb/assets/99473954/6e659246-9eff-46bc-9fd1-efbcc7ba42d7)
  ![page web PHP](https://github.com/GrandNabil/testserveurweb/assets/99473954/ce3670b5-0747-43a4-b6bb-29ecb1b325df)

- Installation du gestionnaire de base de données MariaDB et installation minimale de sécurité en répondant aux questions de sécurité.

  ![MariaDB](https://github.com/GrandNabil/testserveurweb/assets/99473954/e7af5a1d-e2de-4d35-9508-3f5244956fac) 
  ![MariaDB](https://github.com/GrandNabil/testserveurweb/assets/99473954/eab61de8-4311-4e43-9c42-9cdf6cfe1a3c)
  ![MariaDB](https://github.com/GrandNabil/testserveurweb/assets/99473954/a392f875-db1b-4f4d-b5ba-8bdf6118f0fd)

- Installation de Wordpress
  On commence d'abord par une création de la base de données pour WordPress qui va stocker toutes les informations liées à la configuration et au contenu du site web. Ensuite, je crée un utilisateur qui est l'administrateur avec tous les privilèges pour opérer sur la base de données.

  ![base de données du site](https://github.com/GrandNabil/testserveurweb/assets/99473954/fb69b118-bff2-4ab7-ae90-1367ac033d47)

  Nous allons utiliser le site par défaut d'Apache "/var/www/html" pour stocker les données du site WordPress en le remplaçant par le site WordPress.
  D'abord, je télécharge le fichier zip de WordPress. Ensuite, je décompresse avec l'outil Zip. Puis, je déplace le dossier WordPress vers '/var/www/html' et enfin, je donne les droits d'utilisateur au serveur Apache pour préciser que c'est le serveur web. 'sudo chown -R www-data:www-data /var/www/html/'
  Vérification ensuite de l'installation.

  ![Installation de WordPress](https://github.com/GrandNabil/testserveurweb/assets/99473954/cbca250a-ccfe-49f0-8a18-cc31cbcb46e8)
  ![Installation de WordPress](https://github.com/GrandNabil/testserveurweb/assets/99473954/9c50c258-fc57-49f4-a819-570ed116351f)
  ![Installation de WordPress](https://github.com/GrandNabil/testserveurweb/assets/99473954/1ae66a02-32be-45eb-bf3e-1bf8dae27bcc)

- Configuration de Wordpress

  Pour accéder à WordPress sur un navigateur, j'ai utilisé l'adresse publique du serveur.
  Cette étape consiste à choisir la langue de l'interface.

  ![Page d'accueil de configuration de WordPress](https://github.com/GrandNabil/testserveurweb/assets/99473954/b02bdc6d-7d21-4352-874a-3bd6204d823e)

  La page de bienvenue qui nous informe sur ce qui va suivre.

  ![Page de bienvenue](https://github.com/GrandNabil/testserveurweb/assets/99473954/01ba89ea-e62a-422e-bb3e-db387cc32cd3)
  
  Les informations de connexion à la base de données.

  ![Détails de connexion à la base de données](https://github.com/GrandNabil/testserveurweb/assets/99473954/8b5143dc-0f4a-477f-9655-107216b13674)

  Les informations de connexions pour le site WordPress. Pour les besoins du test, j'ai utilisé des noms de connexions assez évidents.

  ![Informations pour le site WordPress](https://github.com/GrandNabil/testserveurweb/assets/99473954/1b6fdafb-bc6a-437d-b19f-34b1675f5e8b)

  ![Page de succès](https://github.com/GrandNabil/testserveurweb/assets/99473954/6f031238-402e-4b50-8648-3bc212ada66b)

  ![Dashboard WordPress](https://github.com/GrandNabil/testserveurweb/assets/99473954/e86504f0-13a4-4029-a893-18862fd7a71f)
  
  ![Page d'accueil du site](https://github.com/GrandNabil/testserveurweb/assets/99473954/e28bef3d-d39d-4238-8dc0-10590b101006)

  Suppression du fichier temporaire "wp-config-sample.php", car il n'a plus d'intérêt, le fichier wp-config.php est maintenant définitif. On met en lecture seule le fichier "wp-config.php". Il contient les informations sensibles en rapport avec le site et la base de données. 

  ![Modification de sécurité](https://github.com/GrandNabil/testserveurweb/assets/99473954/037237ee-c5ad-4d1e-ab95-f971c848b7c2)

  Installation des extensions pour assurer la sécurité du site.

  ![Les extensions](https://github.com/GrandNabil/testserveurweb/assets/99473954/6595e953-4ff3-4d20-8ea8-7fc77486cf53)

  Je suis à la fin de l'installation et du déploiement du site web Wordpress.
  J'ai d'abord configuré la sécurité de mon serveur ubuntu en:
  - changeant le mot de passe root;
  - désactivant la connexion ssh au serveur par mot de passe;
  - désactivant les ports inutilités pour ensuite autoriser uniquement les ports souhaités
  - Faisant chaque fois la mise à jour des paquets
    Ensuite j'ai installé le serveur LAMP. Pour le faire :
    - J'ai installé le serveur web apache avec les configurations de sécurité à savoir: vérification de la version d'apache(mise à jour si ce n'est pas la dernière), a2enmod ssl' pour gérer les certificats SSL, restrictions des accès aux fichiers en ajoutant des règles dans le fichiers de confoguration apache.
    - J'ai installé le moteur de script php qui est très utile surtout pour les site web wordpress
    - J'ai installé et configurer la base de données MariaDB avec la configuration minimale de sécurité en répondant aux questions posée lors de la configuration
    - J'ai installé et configuré Wordpress
  Enfin j'ai déployé le site web qui est accesible depuis le serveur.
