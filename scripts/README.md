# Kubectl extension - Kubplugin

By thinking of core kubectl commands as essential building blocks for interacting with a Kubernetes cluster, a cluster administrator can think of plugins as a means of utilizing these building blocks to create more complex behavior. Plugins extend kubectl with new sub-commands, allowing for new and custom features not included in the main distribution of kubectl.

## Installing your plugin
You can write a plugin in any programming language or script that allows you to write command-line commands.

There is no plugin installation or pre-loading required. Plugin executables receive the inherited environment from the kubectl binary. A plugin determines which command path it wishes to implement based on its name. You must install the plugin executable somewhere in your PATH.

As seen a plugin determines the command path that it will implement based on its filename. Every sub-command in the command path that a plugin targets, is separated by a dash (-). For example, a plugin that wishes to be invoked whenever the command kubectl kubplugin is invoked by the user, would have the filename of kubectl-kubplugin

- To use a plugin, make the plugin executable:
    `sudo chmod +x ./kubectl-kubplugin`

- Next step, place it in your `PATH`:
    `sudo mv ./kubectl-kubplugin /usr/local/bin`

- You may now invoke your plugin as a kubectl command:
    `kubectl kubplugin <RESOURCE_TYPE> <NAMESPACE>`

- cYou can check that kubectl recognizes your plugin:
    `kubectl plugin list`