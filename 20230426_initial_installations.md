# Initial installations on a new Ubuntu

## Install Vim

```
$ sudo apt install vim
```

## Change bash aliases

Commented out:

```bash
# some more ls aliases
# alias ll='ls -alF'
# alias la='ls -A'
# alias l='ls -CF'
```

And added the following to `~/.profile`:

```
alias la="ls -lah"
alias profile="vim ~/.profile"
alias sprofile="source ~/.profile"
```

## Install ssh server

```bash
$ sudo apt install openssh-server
$ sudo systemctl enable ssh
$ sudo systemctl start ssh
```

## Added new script to add ssh user

```bash
$ cd ~
$ mkdir utilities
$ cd utilities
$ touch createsshuser.sh
$ chmod u+x createsshuser.sh
```

And put in `createsshuser.sh` the following:

```bash
#!/bin/bash

USER="$1"
shift
SSH_PUBLIC_KEY="$*"

PASSWORD=$(cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 32 | head -n 1)
echo "password for user '$USER' is '$PASSWORD'"
echo "also has public key: "
echo $SSH_PUBLIC_KEY

# create a user with a random password
adduser ${USER}

echo "...changing password now to '$PASSWORD'"
echo ${USER}:${PASSWORD} | chpasswd

# add the user to the wheel group so they can sudo
echo "...adding user to sudo group"
usermod -a -G sudo ${USER}

# add the ssh public key
echo "...adding public key to user's authorized_keys"
su - ${USER} -c "umask 022 ; mkdir .ssh ; echo $SSH_PUBLIC_KEY >> .ssh/authorised_keys"
```

## Install python3.11

```bash
$ sudo add-apt-repository ppa:deadsnakes/ppa
$ sudo apt install python3.11
```

Add options to `python3`, allowing switch to `python3.11`

```bash
$ sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.10 1
$ sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.11 2
```

Choose which by using commad:
```bash
$ sudo update-alternatives --config python3
```

Looks like Ubuntu currently doesn't play nice with 3.11 so keeping default to 3.10

### Install pip for python3

```bash
$ sudo apt install python3-pip
```

### Install venv

```bash
$ sudo apt install python3.10-venv
```

## Install fastapi, slack

```bash
$ python3 -m pip install fastapi[all]
$ python3 -m pip install slackclient
$ python3 -m pip install slackeventsapi
```

## Install git 

```bash
$ sudo apt install git
```