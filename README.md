# OpenStack-CLI in a box

Someone probably sent you a link to this repository, to get you up and running using an openstack cloud. So, let's get started.

---

## Requirements?

- [Visual Studio Code](https://code.visualstudio.com)
- The [Remote-Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension
- Docker ([Docker Desktop](https://www.docker.com/products/docker-desktop) on Windows/Mac OSX, [Docker CE/EE](https://docs.docker.com/get-docker/) on Linux)

---

## Template?

**Why is this a template?** 

Simple: You can add the public details of your cloud provider to your version of this repository and share that one with, for example, your coworkers.

---

## Step by Step

- Create your own version of this repository - the green `Use this template` button on top 
- In Visual Studio Code, use `Clone Repository in Container Volume` from the command palette and paste the URL of your copy
- Wait. Like 2-3 minutes, while VSCode does its magic.

You can also clone your repository locally, open it in vscode and confirm the popup question about reopening in the container. Personal preference.

---

## The configuration

For reference, have a look into the [official documentation](https://docs.openstack.org/python-openstackclient/latest/cli/man/openstack.html#cloud-configuration).

First, change the file `clouds-public.yaml` in this repository to fit your cloud configuration, leaving out all personal details. You can add multiple entries, as you need them. You should commit this file, it can be used by coworkers for example.

Next, create a new file `clouds.yaml` next to it, adding all the private details. Same as above, you can add multiple identities here.
```yaml
clouds:
  myaccount:
    cloud: mycloud      # The name of the cloud defined in clouds-public.yaml
    auth:
      username: username
      project_id: id
      project_name: project-name
      password: "secret"
```
This file should **never** be commited!

---

## Use it!

Open an **integrated** terminal.

Enable your selected cloud identity by `export OS_CLOUD=myaccount`, using your chosen name for the identity.

The example `myaccount` is already enabled.

All available tools are now using this profile.

```
 $ openstack server list
+--------------------------------------+-----------+--------+--------------------+--------------+-----------+
| ID                                   | Name      | Status | Networks           | Image        | Flavor    |
+--------------------------------------+-----------+--------+--------------------+--------------+-----------+
| f0935676-9c3f-4dc1-801a-c2972a1affa5 | example   | ACTIVE | prod=192.168.1.140 | Ubuntu 21.10 | m1.medium |
+--------------------------------------+-----------+--------+--------------------+--------------+-----------+
```

---

## What's included?

- The OpenStack SDK / CLI (`openstack`)
- Terraform (`terraform`)

To be extended...

---

## Extending it?

Sure, go ahead! There are so many options here!

Need ansible? Add it to the `requirements.txt`.

Need another package? `.devcontainer/Dockerfile` is the place to go.

Environment variables? Look into `.devcontainer/devcontainer.json`.

SSH-Keys? Try `ssh-add -l` in the integrated terminal! (If you don't get results, make sure your ssh-agent on your host is working - VSCode takes care of the rest).

Want to personalize the container? That's a topic by itself. -> [Starting point!](https://code.visualstudio.com/docs/remote/containers#_personalizing-with-dotfile-repositories)

And not to forget: When you changed something, run `Remote Containers: Rebuild container` from the command palette! Your workspace (in `/workspaces`) will remain untouched!