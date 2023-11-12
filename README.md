# Terraform Beginner Bootcamp 2023

## Semantic Versioning :mage:

This project is going to use semantic versioning for its tagging.
[semver.org](https://semver.org/)

The general format: 
**MAJOR.MINOR.PATCH**, eg. `1.0.1`

- **MAJOR** version when you make incompatible API changes
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes

## Install The Terraform CLI

### Consideration with the Terraform CLI changes

The Terraform CLI installation instructions have changed due to gpg keyring changes. So we needed to refer to the latest install CLI instructions via Terraform Documentation and change the scripting for install.

[Install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

### Consideration for Linux Distribution.

This project is built against ubuntu.
Please consider checking your Linux Distribtion and change accordingly to distribution needs. 
[How to check OS version in Linux](https://linuxize.com/post/how-to-check-linux-version/)

Example of checking OS version:
```
$ cat /etc/os-release
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

## Refactoring into Bash Scripts

While fixing the Terraform CLI deprecated issues we noticed that the bash scripts steps were a considerable amount more code. So we decided to create a bash script to install the Terraform CLI.

This Bash Script is located here: [./bin/install_Terraform_cli](./bin/install_terraform_cli)

- This will keep the Gitpod Task File ([.gitpod.yml].gitpod.yml) tidy.
- This allow us an easier to debug and execute manually Terraform CLI Install.
- This will allow better portability for other projects that need to install Terraform CLI. 

#### Shebang Considerations


A Shebang (pronounced Sha~bang) tells the bash script what program will interpret the script. eg. `#!/bin/bash`

ChatGPT recommended this format for bash: `#!/usr/bin/env bash`

- for portability for different OS distribution.
- will search the users PATH for the bash executables

https://en.wikipedia.org/wiki/Shebang_(Unix)

#### Execution Considerations

When executing the bash script we can use the `./` shorthand notation to execute the bash script.

eg. `./bin/install_terraform_cli`

If we are using a script in .gitpod.yml we need to point the script to a program to interpret it.

eg. `source ./bin/install_terraform_cli`

#### Linux Permissions Considerations

Inorder to make our bash script executable we need to change linux permission for the fix to be executed at user mode.  

```sh
chmod u+x ./bin/install/install_terraform_cli
```

alternatively:

```sh
chmod 744 ./bin/install/install_terraform_cli
```

https://en.wikipedia.org/wiki/Chmod

### Github Lifecycle (Before, Init, Command)

We need to be careful when using the Init because it will not rerun if we restart an existing workspace.

https://www.gitpod.io/docs/configure/workspaces/tasks