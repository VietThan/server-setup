# 2023-05-12: Collection of stuff did since last time

## Script to create new user with ssh
```shell
$ cd
$ mkdir utilities
$ cd utilities
$ touch createsshuser.sh
```

Contents of `createsshuser.sh`:

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
su - ${USER} -c "umask 022 ; mkdir .ssh ; echo $SSH_PUBLIC_KEY >> .ssh/authorized_keys"
```

Usage example
```bash
$ sudo ~/./utilities/createsshuser.sh nicholasg ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDPpCohquTpbMOB6r4juvE869vvZ61f5iLwq0M+KrP7vr564OCMJonDLF/m4csWcrcLi3hRoH9dWmXjvmaRroxnB06Vv1zM74icSUK+4uYajYl25biIPrrYPJCGs1adKVgjyGalQ1YhfzZJ7gT3zeO/2pV4cTCxPONB1GCFyQ9t1y0ruaEffFPoKBSA8+zL8oILQ1Rk9k6xghkPFtc9+ljYBjatLZ86ZUpoaY+u9TowgCeyPSZD57GoJi/hsXHO99Er5ZEaYOh93QzRiBqSXJoSdjXYenHYhnz8qCzOglIyByJtrznBiw3+2zO/8QN0jUU7ysOZibc0mxAUMe7DHxLJUi7+3WFAiPHIN01xYwJmdZX1EtPD+QkPORxxE+TuSgwEPY3s2jMGbO2yw7w8e3Kb2BFSZi5/jwplxne0wpOoaz8qhmRhL0u9ZJiQOdXRlAja7SD1zqDMcGcM9ANWQeQtBSEsBDCBbiCkRiaFJx5ID3Mwngr59pXuvUhqj8RUaRU= nicholas@MacBook-Air.localdomain
```