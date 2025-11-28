# Prerequisites

To use the CLI, you must have an OS which is supported by the cli
(see [download page](https://cli.fundamentum-iot.com)). You must also have a Fundamentum
account with the permissions required for the functionalities you want to use.

# Installation

It's available [here](https://cli.fundamentum-iot.com)

# Authentication

You can authenticate the cli with the command `fun login`. It will ask you a few questions
necessary to configure an authentication context for the app, like endpoints and context
name. The default values are fine for Fundamentum deployed on fundamentum-iot.com (Just 
press enter to accept the defaults). It will then open a web browser to the Fundamentum
login page and wait for you to login (or it will close this page directly if you are
already logged in). In either way, it will get an authentication token from Fundamentum
and save it in the local context.

Later, each time you use the CLI, the context with the name 'default' will be used. If
you have multiple contexts (different users or connections), you can use this specific
context instead of the default one by appending its name to the command. Example:

`fun functions list --project 1 --context [CONTEXT_NAME]`

