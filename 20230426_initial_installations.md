# 2023-04-27: Initial installations on a new Ubuntu

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