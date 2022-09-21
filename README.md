# My Docker Development Environment

This is a repo for creating a docker image which I use to develop my research projects. It is not for deployment, and typically neither are the applications developed using it. It is not intended to be lightweight or plug-and-play ready, but where possible, I tried to make it extensible for other users.

## Features

#### SSH & SFTP Access
A non-privileged run of `sshd` on the container. combined with port forwarding on a non-privileged port like `2022`, this allows direct `ssh` and `sftp` access to the container, useful for setting up a remote interpreter in PyCharm.

##### Relevant Files
- `Dockerfile`: installs and sets up sshd, including the default command to run it on container launch (need to set this as part of the command as well when running in k8s)
- `sshd_config`: the config copied into place for the running `sshd` service
- `sshd-1.service`: a service definition for our non-privileged run of `sshd`
- `id_rsa.pub`: MY ssh public key. Replace with yours!

### Miniconda

Miniconda pre-installed, no significant packages added. Images should extend this one and run conda environment set up.

### github.com known hosts

See warning about the security of this, this bypasses the fingerprint check in git clone via ssh by pre-loading the public keys for github.com, so that a repo can be clone on container start. You're implicitly trusting that I did this correctly, see [this ServerFault discussion](https://serverfault.com/a/701637) for details.

### ZSH and oh-my-zsh

I install zsh and my own personal dotfile preferences, only some of which are generally applicable. Adjust or remove as needed.

### (my) ssh config

I found it useful to be able to ssh from my container to other hosts I use, especially for copying files while debugging and/or placing them in a mounted volume. Remove this build step if it doesn't sound useful or replace with your own config.
