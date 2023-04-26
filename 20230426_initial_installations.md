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
