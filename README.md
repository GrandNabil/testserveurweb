# testserveurweb

### Etape 1: Préparation et Endurcissement du Serveur

#### Installation du serveur Linux:
Ici le serveur mis à ma disposition est un serveur ubuntu.

#### Check-list de sécurisation du serveur
- Modification du mot de passe root (changeme) par un mot de passe complexe(258oO#Test)
    Je fais cette modification pour éviter l'utilisation non autorisée du compte super utilisateur.
  
    ![modification de mot de passe](https://github.com/GrandNabil/testserveurweb/assets/99473954/b3650936-2e92-4205-8717-c2171d2a194a)
  
- Désactivation de la connexion SSH par mot de passe & Changement du port SSH 22. Le choix du port est 11592.
  Je fais cette désactivation parce que avec la connexion par mot de passe, il y a plus de risque qu'il soit découvert.
  La connexion par clés publiques/privées a été déjà configuré  ici l'outils utilisés pour le faire est openssl.
  Le port 22 est connu par défaut comme le port SSH, donc je le change par un autre numéro de port afin d'éviter les tentatives de connexion.
  Installation de OpenSSH-server pour nous permettre d'utiliser le protocole SSH.
  
     ![désactivation et changement de port](https://github.com/GrandNabil/testserveurweb/assets/99473954/85d86fde-d988-46ec-8fbf-d5301e1dacbc)

  J'ai modifié le fichier `etc/ssh/ssh_config` pour la désactivation de la connexion par SSH et le changement de port SSH

- Désactivation des ports inutilisés (FTP, HTTP, Telnet, etc.)
  Par défaut, les ports sont ouverts et pour une meilleure sécurité, je ferme les ports qui ne seront pas utilisés ici.
  Pour le faire, j'utilise le pare-feu UFW. UFW parce que c'est simple à utiliser et il permet de créer des règles efficaces.
  Je bloque par défaut les connexions entrantes et j'autorise les connexions sortantes
  Ensuite j'autirse ssh sur le nouveau port, https, htpp, mysql pour les services web. Je m'en arrête là. S'il y'a dautres règles après elles seront ajoutées

  
    ![Configuration Pare-feu)](https://github.com/GrandNabil/testserveurweb/assets/99473954/48e71a38-a59b-4159-8ae6-15930ae6ec59)
    ![Configuration Pare-feu](https://github.com/GrandNabil/testserveurweb/assets/99473954/3e1cde96-6001-45ad-bb5f-bcc900c241be)


- Faire la mise à jour des paquets et vérifer qu'ils sont à jours. 

  
