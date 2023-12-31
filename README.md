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


### Workng with Env Vars

#### env command

We can list out all the environment variables (Env Vars) using the 'env' command

We can filter out specific env vars using grep eg. 'env | grep AWS_'

#### setting and unsetting the Env Vars

In the terminal we can set using 'export='HELLO='world'

In the terminal we can unset the 'unset 'HELLO'

we can set env var temporarily when just running a command 

```sh
HELLO='world' ./bin/print_message
```

Within a bash script we can write env variables without using export eg.
```sh
#!/usr/bin/env bash

HELLO='world'

echo $HELLO
```

#### Printing vars 

We can print env vars using echo eg. 'echo $HELLO'


#### Scoping of Env Vars

When you open up new bash terminal in VSCode it will not be aware of env vars that you have set in another window 

If you wnat to Env Var to persist across all the future bash terminal that are open you need to set env var in your bash profile. eg. '.bash_profile'


#### Persisting Env Vars in gitpod

We can persist Env vars in gitpod by storing them in Gitpod secret storage.

```
gp env HELLO='world'

```

All future workspaces launch will set the Env Var to the bash terminals opened in those workspaces.


you can  also set env var in '.gitpod.yml' but this can only containt non-sesitive environments variable.


### AWS cli installation 

AWS cli is installed for the project via the bash script ['./bin/install_aws_cli'](./bin/install_aws_cli)

[Getting started install (AWS cli)] (https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html#getting-started-install-instructions)
[AWS CLI env vars] (https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html)


We can check if our AWS cridentials configured correctly by running the following command 
AWS CLI command:
```sh
aws sts get-caller-identity
```

If it is succsessful you should see the Json paylod that looks like this: 
```json
 "UserId": "AIDAZ2JXGRjhbucy774ubed",
 "Account": "1122667792929",
 "Arn": "arn:aws:iam::bwdd83u8:user/terraform-begginer-bootcamp"
 ```

 We will need to genrate AWS cli credentials from IAM user in order to AWS CLI.