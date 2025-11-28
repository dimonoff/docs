# Environment variables

By default, the cli executes in interactive mode (asking for input as needed).

It is possible to use the CLI in an environment where user interaction is not possible
(for example, in a script). In this case, you need to provide what the CLI requires via
environment variables. Example:

`fun functions list --project 1`

needs an authentication context. So you can use it that way:

```
export FUN_CONTEXT_API_KEY={YOUR_API_KEY}
export FUN_CONTEXT_FUNCTIONS_ENDPOINT=https://functions.fundamentum-iot.com
export FUN_CONTEXT_FUNDAMENTUM_IOT_ENDPOINT=https://api.fundamentum-iot.com
fun functions list --project 1
```

The cli will use an anonymous context made up of values provided by environment variables.

It's also possible to specify certain environment variables for certain commands. You can
view the [command reference](https://cli.fundamentum-iot.com/reference/fun.html) for more information on this (english only).

# Configuration location

The Fundamentum CLI will look for its configuration files in the following places (highest to lowest priority)

1. the value of `--config`, if specified
2. the environment variable `FUN_CONFIG_DIRECTORY`
3. `$XDG_CONFIG_HOME/fun/` (by default, `$HOME/.config/fun/`)
4. `$XDG_CONFIG_DIRS/fun/` (by default, `/etc/xdg/fun/`)
5. `./.fun/` (to be portable, by having configuration relative to the cli)