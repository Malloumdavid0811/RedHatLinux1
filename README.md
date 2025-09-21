# THEMATIQUE: Projet personnel sur "Red Hat Linux" avec HAProxy pour la haute disponibilité des serveurs web 

Dans ce TP, nous allons voir comment mettre en place une architecture web haute disponibilité.

La répartition de charge est donc une des technologies qui participe à la haute disponibilité.

Elle s’entend le plus souvent au niveau des serveurs HTTP (par exemple, sites à forte audience devant pouvoir gérer des centaines de milliers de requêtes par secondes), c’est-à-dire en frontal sur une plate-forme web comme nous allons le mettre en œuvre dans ce TP. Mais le même principe peut s’appliquer sur n’importe quel service aux utilisateurs ou service réseau.

Ce TP aura pour but de Caractériser les éléments nécessaires à la qualité et à la continuité d'un service, Installer et configurer les éléments nécessaires à la qualité et à la continuité du service, Contrôler et améliorer les performances d’un service, Valider et documenter la qualité et la continuité.

Il vous permettra de savoir définir des éléments nécessaires à la continuité d'un service :

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


### b) Création du Dockerfile de l'application flask

![1756133497949](https://github.com/user-attachments/assets/c651ff06-19f8-4ce6-9cc7-3ed2932ec720)

### c) Build de l'image student-age

![1756133508706](https://github.com/user-attachments/assets/b2e30cc3-6b95-4c97-bbaa-3178cbe5e5c2)

### d) Création du fichier docker-compose

![1756133533330](https://github.com/user-attachments/assets/d4d7b905-7888-4db6-8146-61e76edc0ed0)

### e) Déploiement de notre stack applicative frontend et backend avec docker-compose

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

![1756133692067](https://github.com/user-attachments/assets/e06c6b73-f947-414e-ae2d-da58e990502b)

![1756133704694](https://github.com/user-attachments/assets/9484551f-907b-47c2-8bff-e9c1d479fc73)

![1756133716818](https://github.com/user-attachments/assets/67b4a35b-794f-4e17-8538-72be60a17dad)

![1756133728422](https://github.com/user-attachments/assets/7540b704-63f9-44cf-ab41-eac3094e09aa)

![1756133741689](https://github.com/user-attachments/assets/1d0a5e01-c19d-4568-83c5-851e20f92164)







