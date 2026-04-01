# À propos de ce guide

## Chapitres et titres de sections

Les chapitres correspondent aux pages principales du menu principal de gauche de la plateforme (encadrés en rouge). Les sections, elles, aux différentes options et fonctionnalités que comportent ces pages.

<figure><img src="../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>



**Note** : En fonction de la licence sélectionnée, il est possible que tous les menus de gauche ne soient pas disponibles. Les menus « Accueil » et « Inventaire » sont les deux seuls présents par défaut dans la plateforme. Contactez votre représentant Dimonoff si certains menus nécessaires n’apparaissent pas.



## Entités de la solution

<table data-header-hidden><thead><tr><th width="213"></th><th></th></tr></thead><tbody><tr><td>Entité</td><td>Explication</td></tr><tr><td>Licences</td><td>Une licence est une entité semblable à un conteneur. Elle peut par exemple représenter un client, une unité d’affaires, une ville, une municipalité ou un groupe important de bâtiments. <br>Pour plus d’informations, veuillez vous référer à la section "Architecture d’un projet" ci-dessous.</td></tr><tr><td>Objets  ou Actifs</td><td>Un objet est un appareil qui exécute une fonction spécifique dans une zone géographique. Par exemple, un objet peut être un écran d’affichage dynamique, une borne de paiement ou un capteur de détection d’état de stationnement. <br>Pour plus d’informations, veuillez vous référer à la section "Comprendre le système de détection d’état de stationnement Dimonoff" dans le chapitre "À propos de Spatium".</td></tr><tr><td>Lieu<br></td><td>Un lieu est un point géographique dans une licence contenant un nombre de zones. Sur une carte, il apparaît comme un pin défini par des coordonnées géographiques sur lequel l’utilisateur peut cliquer pour y entrer. <br>Pour plus d’informations, veuillez vous référer à la section "Architecture d’un projet" ci-dessous.</td></tr><tr><td>Zone<br></td><td>Une zone est une aire géographique qui contient un certain nombre d’objets connectés et/ou non connectés. Sur la carte, la zone apparaît comme une aire ombragée et fermée, définie par des coordonnées géographiques et contenant des objets. <br>Pour plus d’informations, veuillez vous référer à la section "Architecture d’un projet" ci-dessous.</td></tr><tr><td>Groupe</td><td>Vous pouvez grouper les places de stationnement pour répondre à plusieurs usages de gestion, tels qu’afficher vos sections réelles sur le plan de stationnement, obtenir la disponibilité de vos groupes ou sections de façon plus granulaire, créer des rapports relatifs à vos groupes ou segmenter vos zones en groupes pour les lier à des panneaux dispersés dans vos allées. <br>Pour plus d’informations, veuillez vous référer à la section "Grouper des places" dans le chapitre "Inventaire".</td></tr><tr><td>Place<br></td><td>Une place est un emplacement de stationnement en rue ou sur un plan. Elle peut être de différents types comme : normale, réservation, véhicule électrique, pour personnes handicapées, VIP, etc. Plusieurs places peuvent être liées à un même capteur : 2 places maximum par capteur MPS ou jusque des centaines pour une caméra. <br>Pour plus d’informations, veuillez vous référer à la section "Configurer des places de stationnement" dans le chapitre "Inventaire".</td></tr></tbody></table>



## Architecture d’un projet

Dans les concepts de base, nous avons vu que la plus haute entité de l’architecture est une licence. Celle-ci représente en fait un client et est constituée de lieux. Chaque client peut avoir plusieurs licences.

À partir de celle-ci, illustrons l’architecture des projets dans Spatium:

<figure><img src="../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>



En tant qu’administrateur de la plateforme Spatium, vous pourrez créer, modifier, supprimer tous lieux et/ou zones ainsi que ce qui les constitue (places de stationnement, barrières d’accès, panneaux de jalonnement, etc.) dans vos différentes licences.

