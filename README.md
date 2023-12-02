# Terraform Beginner Bootcamp 2023

## sementic versioning :mage:

This project is going to utilize sementic versioning for its tagging.
[semver.org](https://semver.org/)

The genral example:
 **MAJOR.MINOR.PATCH,** eg. `1.0.1`

- **MAJOR** version when you make incompatible API changes
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes

## Install the terraform cli

### Considrations with the terraform CLI changes
The terraform CLI installations instructions have change due to gpg keyring changes. So we need to reffer the latest terrafform CLI installation instructions via official terraform documentation and change the scripting for install.

[Install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)


### This considration is for Linux distribution
This project is build agains the ubuntu distribution needs. So check the needs of your distribution and change according.

[How to check OS version in Linux](https://www.ionos.com/digitalguide/server/know-how/how-to-check-your-linux-version/#:~:text=The%20command%20%E2%80%9Cuname%20%2Dr%E2%80%9D,the%20Linux%20kernel%20is%205.4.)

Example of checking OS version:

```
$ cat /etc/os-release

PRETTY_NAME="Ubuntu 22.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.3 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
```

### Refactoring into bash scripts

While fixing the terraform CLI gpg depriciation issue. We noticed that bash script steps were considerable amount of more steps. So we decided to create a bash script to install terraform CLI.

This bash script is located here: [./bin/install_terraform_cli](./bin/install_terraform_cli)



- This will keep the gitpod ([.gitpod.yml](.gitpod)) task file tidy.
- This will allow us to easier to debug and execute manually terraform CLI install.
- This will allow better portablity for the other projects that needs to install terraform CLI.


### shebang considration

A shebang (pronounced as sha-bang) tells the bash script what program that will interpret the script. eg.`#!/usr/bin/bash` 

ChatGPT recommened this format for bash. eg. `#!/usr/bin/env bash`

- For portablity for diffrent OS distribbution.
- Will search the user's path for the bash executable.


#### Execution considration


When executing the bash script we can use `./` shorthand notaion to execute the bash script.

eg. `./bin/install_terraform_cli`

If we are using script in .gitpod.yml then we need to point the script to interpret it.

eg. `source ./bin/install_terraform_cli`

https://en.wikipedia.org/wiki/Shebang_(Unix)



#### Linux considrations

In order to make script executable we change the permissions accordingly to make it executable at the user mode.
```sh
chmod u+x ./bin/install_terraform_cli
```

Alternatively 
```sh
chmod 744 ./bin/install_terraform_cli
```
https://en.wikipedia.org/wiki/Chmod


### GitHub Lifecycle (before, init, command)

We need to be careful when using the init because it will not return if we restart exsisting workspace.

https://www.gitpod.io/docs/configure/workspaces/tasks