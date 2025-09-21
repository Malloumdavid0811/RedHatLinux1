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

## 3) Mise en place d’HAProxy :

Nous allons maintenant intégrer le nouveau service HAProxy.

### a) Sur notre troisième serveur, installons HAProxy

![1758423418819](https://github.com/user-attachments/assets/cf0dc0af-d8bd-4bb0-a01a-318784bfda9c)

### b) Avec de la documentation que nous retrouverons sur le net, mettons en place un logging de notre HAProxy, qui permettra de tracer et de stocker tous les logs dans « /var/log/haproxy.log »

![1758423431770](https://github.com/user-attachments/assets/fe7926f8-32f2-4992-af46-f1a931fd067d)

![1758423442965](https://github.com/user-attachments/assets/a2e51435-7447-4813-a574-c86fbd5e9a14)

![1758423460418](https://github.com/user-attachments/assets/3e8dcb9e-83e7-4019-aa97-b2325d3524f1)

### c) Démarrons notre HAProxy, et assurons-nous qu’il est bien fonctionnel (faire une requête curl sur notre service HAProxy)

Un fichier de configuration HAProxy est composé de sections telles que frontend, backend, default, global et listen.

Chaque section à une fonctions bien particulière dans l’utilisation du HAProxy, ainsi :

o global : La section global apparaît en haut de votre fichier de configuration. Elle définit les directives au niveau du processus telles que le nombre maximum de connexions à accepter, l'emplacement de stockage des journaux et l'utilisateur et le groupe sous lesquels le processus doit s'exécuter.

o backend : Une section backend définit un pool de serveurs vers lesquels l'équilibreur de charge acheminera les requêtes, Vous pouvez ajouter autant de sections backendque nécessaire. Chaque mot-clé backend est suivi d'une étiquette, telle que web_servers, pour le différencier des autres.

o frontend : Une section frontend définit les adresses IP et les ports auxquels les clients peuvent se connecter, Vous pouvez ajouter autant de sections frontales que nécessaire pour exposer divers sites Web ou applications sur Internet.

o default : Une section default stocke les paramètres communs qui seront hérités par les sections frontend et backend qui la suivent, elle offre un moyen de condenser de longues configurations en réduisant les lignes dupliquées.

o listen : Une section listen définit un proxy complet avec son frontend et son backend combinées en une seule section., elle est généralement utile pour le trafic TCP uniquement.

![1758423477781](https://github.com/user-attachments/assets/b3fc750b-4066-4b6e-8e99-7d7467dc2184)

### d) Procédons à une première configuration d'HAProxy avec mise en place des d’un « backend » nommé « my-backend », qui fera du round robin sur vos deux serveurs web 1 et 2, et avec un check sur ces deux serveurs ; Rajoutons sur notre section « frontend » une directive « default_backend » qui pointera sur notre nouveau backend fraichement configuré et trouvons la bonne commande nous permettant de vérifier que la configuration de notre fichier est valide (commande proposée par HAProxy)

![1758423488627](https://github.com/user-attachments/assets/ef55d890-9d28-4b92-b68f-081baef855bd)

### e) Redémarrons notre HAProxy, et assurons-nous que cette fois les requêtes sont bien loadbalancé sur nos deux serveurs web (faire des tests avec des requêtes curl)

![1758423506572](https://github.com/user-attachments/assets/7eb9c379-90c6-41d0-b1fe-5b9ca80fc3a0)

## 4) Mise en place des stats :

Nous allons maintenant passer aux stats sur votre architecture et de votre flux.

HAProxy permet d'afficher une interface regroupant l'ensemble des statistiques du service (frontend, backend, etc.).
Ceci pouvant être utile afin de s'assurer de la bonne répartition de charge ou simplement du bon fonctionnement du service.

### a) Avec de la documentation que nous retrouverons sur le net, commençons par rajouter une nouvelle section « listen » nommée « stats », dans laquelle nous allons rajouter les bons paramètres pour avoir une url de stats

![1758423517767](https://github.com/user-attachments/assets/bf3c0930-ac51-4fc4-a954-0808ac7eebfb)

### b) Redémarrons HAProxy, et essayons de nous connecter sur cette interface graphique

![1758423528313](https://github.com/user-attachments/assets/bc73d95d-d093-426d-85cc-c98527f1a754)

### c) Changeons les paramètres pour mettre un refresh automatique sur notre interface toutes les 10 secondes

![1758423539723](https://github.com/user-attachments/assets/d566c729-14f7-43ce-83a6-30d850156f71)

### d) Analysons bien l’interface et faisons des tests (test d’arrêt d’un serveur web, requête curl sur le HAProxy et le web, etc…)

![1758423549987](https://github.com/user-attachments/assets/d22178d5-0868-4304-aaa4-1c0bb3a7b0fa)
