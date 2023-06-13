# Pull Multiple Repositories

As the ELISSA packages consist of multiple repositories, it would be helpfull to pull all repositories at once before starting working on the source code. This tutorial presents a possible way of doing this.

---
Table of Content:
- [Pull Multiple Repositories](#pull-multiple-repositories)
  - [Install a Credential and Password Manager](#install-a-credential-and-password-manager)
  - [Use the Terminal Command](#use-the-terminal-command)
  - [Save the Command](#save-the-command)

---
Other usefull pages:

---

## Install a Credential and Password Manager

To avoid a credential check for evrey repository a credential manager would be usefull. A installation guide for the `git-credential-manager` is given [here](https://github.com/git-ecosystem/git-credential-manager/blob/release/docs/install.md). Furthermore a password manager like [`pass`](https://www.passwordstore.org/) must be installed. Use for pass the following command:

```bash
sudo apt-get install pass
```

When the manager is installed a key for *GnuPG* must be generated. Use this command:

```bash
gpg --gen-key
```

You will need to provide a name and a e-mail adress as well as a password. When finished, the key selected to be used during git operations:

```bash
git config --global credential.credentialStore gpg
```

Furthermore the password manager `pass` must be initialized. Use the following command and tabstop to complete the user id:

```bash
pass init
```

## Use the Terminal Command

A terminal command is used to go through all subdirectories and executing a `git pull` command if a `\.git` folder exists there. The command is taken from [this stakoverflow page](https://stackoverflow.com/questions/3497123/run-git-pull-over-all-subdirectories):

```bash
for i in */.git; do ( echo $i; cd $i/..; git pull; ); done
```

To execute the command, run it in the `~/catkin_ws/src/` folder. 

## Save the Command

To execute the command more easily, it can be saved in a `.sh` file in the `~/catkin_ws/src/` folder. To easily run it, it must be executable:

```bash
chmod +x filename.sh
```

It can be executed as shown:

```bash
./filename.sh
```

If you want to use a different command to start it, you can add an alias:

```bash
gedit ~/.bashrc
```

Add this at the end of the file:

```bash
alias <new name>='/home/<full path to script>/filename.sh'
```
