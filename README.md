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

### b) Démarrons nos deux serveurs web, et assurons-nous qu’ils sont bien fonctionnels (regardons les fichiers de logs lors d’une connexion)

Installation de rsyslog sur les deux serveurs

![1758423201964](https://github.com/user-attachments/assets/2cb24536-500d-45aa-a8e0-b1674876d213)

![1758423213281](https://github.com/user-attachments/assets/7e3a968f-ee7f-4092-ac61-4609c00ad81a)

### c) Ajoutons une page web index.html sur nos deux serveurs avec un contenu qui permettra de différencier

![1758423224985](https://github.com/user-attachments/assets/6dac3151-402f-4522-b17d-488141883b00)

![1758423235239](https://github.com/user-attachments/assets/49d0459f-129b-4935-aa2f-672a16ac31f6)

### d) Testons l’accès à nos pages web respectives

![1758423313222](https://github.com/user-attachments/assets/ac16e43c-5e7f-4bbf-bd82-99380156fc0b)

![1758423346256](https://github.com/user-attachments/assets/39cfb2d3-607b-436e-bc66-b4477aed407f)

![1758423392600](https://github.com/user-attachments/assets/59510a3b-9059-4188-a57e-c28078220135)

## 3. Mise en place d’HAProxy :

Nous allons maintenant intégrer le nouveau service HAProxy.

### Sur notre troisième serveur, Installons HAProxy

