# Variables d'environnement

Par défaut, le Fundamentum CLI s'exécute en mode interactif (il vous demandera les
informations dont il a besoin via l'invite de commandes).

Il est possible d'exécuter le Fundamentum CLI dans un contexte où l'intervention humaine
est impossible (dans un script, par exemple). Vous devrez alors fournir au Fundamentum CLI
les valeurs dont il aura besoin via des variables d'environnement. Par exemple:

`fun functions list --project 1`

nécessite un contexte, qui contient les infos d'authentification, et le point d'entrée
des APIs de Fundamentum. C'est donc possible de l'appeler ainsi:

```
export FUN_CONTEXT_API_KEY={VOTRE_CLE_D_API}
export FUN_CONTEXT_NAME=default
export FUN_CONTEXT_FUNCTIONS_ENDPOINT=https://functions.fundamentum-iot.com
export FUN_CONTEXT_FUNDAMENTUM_IOT_ENDPOINT=https://api.fundamentum-iot.com
fun functions list --project 1
```

Il est aussi possible de spécifier des variables d'environnement spécifiques à
certaines commandes. Vous pouvez consulter la [documentation des commandes](https://cli.fundamentum-iot.com/reference/fun.html) à ce sujet (anglais seulement).

# Emplacement

Le fundamentum CLI cherche sa configuration aux emplacements suivants (ordre de priorité):

1. la valeur de `--config`, si spécifié
2. la valeur de la variable d'environnement `FUN_CONFIG_DIRECTORY`
3. `$XDG_CONFIG_HOME/fun/` (par défaut, `$HOME/.config/fun/`)
4. `$XDG_CONFIG_DIRS/fun/` (par défaut, `/etc/xdg/fun/`)
5. `./.fun/` (pour une configuration portable, dans un emplacement relatif)