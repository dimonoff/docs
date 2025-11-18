# Pré-requis

Pour utiliser le cli, vous devez avoir un système d'exploitation compatible
(ils sont listés sur la page de téléchargement). Vous devez également avoir un compte
sur Fundamentum avec les droits suffisants pour les fonctionnalités que vous souhaitez utilisés

# Installation

Il est disponible [ici](https://cli.fundamentum-iot.com)

# Configuration

Il est possible de configurer le cli avec la commande `fun login`. Celle-ci vous
demandera quelques questions, dont les valeurs par défaut sont correctes pour Fundamentum
déployé sur fundamentum-iot.com (Appuyer sur Entrée pour accepter les valeurs par défaut).
Vous serez ensuite redirigé vers la page de connexion de Fundamentum. Après que vous vous
soyez identifiés, votre navigateur se fermera et un contexte sera sauvegardé dans la
configuration locale du cli.

Par la suite, lorsque vous utiliserez le cli, le contexte avec le nom "default" sera
utilisé. Si vous avez de multiples contextes (différents utilisateurs ou connexions),
vous pourrez faire référence à ce contexte par son nom lors de chaque commande. Exemple:

`fun functions list --project 1 --context [NOM_DU_CONTEXTE]`

