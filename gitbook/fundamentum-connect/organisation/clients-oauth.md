# Clients OAuth

**OAuth 2.0** est un protocole d’autorisation qui permet à une application d’accéder de façon sécurisée aux ressources d’un utilisateur sur un service tiers, sans avoir à manipuler directement ses identifiants.

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

**Création d’un nouveau client OAuth 2.0**

1. Cliquer sur “Créer un client OAuth”
2.  Renseigner les champs requis :

    * **Nom** : nom de votre application cliente.
    * **URL de redirection** : **IMPORTANT** — ce champ doit correspondre **exactement** à l’URL de redirection utilisée dans votre application cliente

    <figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>


3. **Une fois le client créé**, le système génère automatiquement :
   * **Identifiant client (Client ID)** : à utiliser dans votre application pour identifier le client auprès du serveur d’autorisation.
   * **Clé secrète client (Client Secret)** : selon le type de flux OAuth implémenté, cette clé peut être requise pour authentifier votre application de manière sécurisée.





