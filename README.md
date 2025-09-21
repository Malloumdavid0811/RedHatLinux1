# THEMATIQUE: Projet personnel sur "Red Hat Linux" avec HAProxy pour la haute disponibilité des serveurs web 

Dans ce TP, nous allons voir comment mettre en place une architecture web haute disponibilité.

La répartition de charge est donc une des technologies qui participe à la haute disponibilité.

Elle s’entend le plus souvent au niveau des serveurs HTTP (par exemple, sites à forte audience devant pouvoir gérer des centaines de milliers de requêtes par secondes), c’est-à-dire en frontal sur une plate-forme web comme nous allons le mettre en œuvre dans ce TP. Mais le même principe peut s’appliquer sur n’importe quel service aux utilisateurs ou service réseau.

Ce TP aura pour but de Caractériser les éléments nécessaires à la qualité et à la continuité d'un service, Installer et configurer les éléments nécessaires à la qualité et à la continuité du service, Contrôler et améliorer les performances d’un service, Valider et documenter la qualité et la continuité.

Il nous permettra de savoir définir des éléments nécessaires à la continuité d'un service :

• Évaluation et maintien de la qualité de service.
• Installation d’une solution d’infrastructure.
• Administration sur site ou à distance des éléments d'un réseau, de serveurs, de services et d'équipements terminaux.

## 1) Architecture et contexte :

Une configuration relativement simple va nous permettre de mettre en œuvre la répartition de charge sur deux serveurs Web préalablement installés.

![1758423108419](https://github.com/user-attachments/assets/bd976b3c-76be-4b1a-951c-fb88e54af885)

La demande de connexion est adressée au serveur HAProxy (coté client) qui détermine, selon l'algorithme configuré, le serveur auquel il va affecter la connexion, parmi les serveurs disponibles (en l'espèce serveur web 1 et serveur web 2).

Une fois la connexion TCP établie, l’équipement de répartition de charge devient pratiquement transparent : dans son rôle de base, il transfère les paquets IP du client vers le serveur sélectionné et vice versa jusqu’à fermeture de la connexion.

### a) Installation de trois machines virtuelles de type Rocky Linux 9

![1758423116890](https://github.com/user-attachments/assets/86cb1437-1051-49e5-84c4-4fa1b89dafaa)

![1758423125536](https://github.com/user-attachments/assets/8775995c-1aa8-4efa-856d-cd04dfc6dfa9)

![1758423134043](https://github.com/user-attachments/assets/6b555d6a-0bbc-4c7a-b570-3aa71d8376d8)

### b) Changement du nom de nos machines et rajout dans le DNS local (/etc/hosts, /etc/hostname)

![1758423141982](https://github.com/user-attachments/assets/9fff0883-86f7-4777-b5c5-b624b8b7b88d)

### c) Assurons-nous que les serveurs sont joignables entre eux (faire des ping pour être sûr)

<img width="588" height="486" alt="Sans titre" src="https://github.com/user-attachments/assets/29f32ee7-1c68-4bba-a112-e0c3c20c14fc" />

## 2. Mise en place des deux serveurs web :

Nous allons dans cette partie mettre en place nos deux serveurs web de type apache.

### a) Installons sur vos deux serveurs web un apache

![1758423171368](https://github.com/user-attachments/assets/2336139b-2399-4ca3-98bf-f1a16d18c78b)

![1758423184265](https://github.com/user-attachments/assets/82c44d90-87c8-4fec-ac81-1fbc7e9d766c)

### b) Déploiement de notre stack applicative frontend et backend avec docker-compose

![1756133542334](https://github.com/user-attachments/assets/e92cc84c-d148-4907-9a60-b53175aafe05)

![1756133553540](https://github.com/user-attachments/assets/16281b14-019a-4905-92fd-cd1914e401be)

![1756133574130](https://github.com/user-attachments/assets/d634876b-f82a-4bf1-a020-341a7258491b)

![1756133583948](https://github.com/user-attachments/assets/11b2045e-dfc6-4367-9e6a-4bd1addef6cc)

### f) Modification de l'index.php

![1756133598081](https://github.com/user-attachments/assets/505f1e2e-26ec-4cd7-a1cd-5af12f6af289)

![1756133608938](https://github.com/user-attachments/assets/2609ad81-57fb-4c24-ba69-306cf3124d79)

### g) Vérification du fonctionnement de l'application

![1756133622919](https://github.com/user-attachments/assets/9eb578de-0c7c-44ef-a825-c3f5cb5e6bee)

### h) Déploiement du régistre privé

![1756133643201](https://github.com/user-attachments/assets/397a42bb-2b6c-4e1f-b1f1-cc86b478470f)

![1756133658156](https://github.com/user-attachments/assets/e2211031-ba37-4133-a23a-e3481d51ac27)

### i) Déploiement de l'IHM (Interface Homme-Machine) du registre privé

![1756133675009](https://github.com/user-attachments/assets/a937db3d-776b-42fc-a1a9-67fa1799ef77)
