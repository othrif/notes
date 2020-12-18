---
title: "ssh keys in remote servers"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: "How to find files using the Linux command line."
type: technical_note
draft: false
---

SSH keys provide an easy, yet extremely secure way of logging into your server. You can following these steps to generate a new SSH key and add it to the ssh-agent:

Run the following command in your terminal: `ssh-keygen -b 2048 -t rsa` For maximum security, you want to generate a 2048 bit RSA key.

You will be prompted to enter a passphrase. It is highly recommended! `~/.ssh/id_rsa.pub` is your public key and `~/.ssh/id_rsa` is your private key. Never share your private key with anyone! 

Next, you will need to upload your ssh public key to your server. Run `cat ~/.ssh/id_rsa.pub | ssh username@remote_host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys”` where you should replace your `username` and `remote_host` accordingly.

Start the ssh-agent in the background by running 


`eval “$(ssh-agent -s)”`
Modify your `~/.ssh/config` file to automatically load keys into the ssh-agent and store passphrases in your keychain

```
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```

Add your SSH private key to the ssh-agent and store your passphrase in the keychain

``` bash 
ssh-add -K ~/.ssh/id_rsa
```

Now you should be able to ssh to your server securely! 


### Access server without ssh keys
If you encounter the error: `Permission denied (publickey).`
``` bash 
sudo emacs /etc/ssh/sshd_config
# Change to: PasswordAuthentication yes
sudo service sshd reload
```
Now if you ssh from a new server, you can access the target server with a password