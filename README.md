# tmux-lan-deploy

A template workspace to work with a shared codebase and terminal across different machines in LAN through nested tmux sessions. 


## Use case

You're really tired and you have:
- Two or more ssh-ready machines in LAN 
- That need to run some platform-specific code 
- Which may or may not be distributed across different packages or repos
- Which may or may not need to be developed in a joint setup

Hence, here is a single workspace:
- Shared in a mount point via sshfs
- In which you can implement your automation scripts
- That call code arbitrarily distributed
- That can run at the same time in different machines


## Dependencies

Assuming all your machines can already connect among them via `ssh`, you may need the following additional packages.

Host machine:
```
$ apt install sshfs openssh-sftp-server \
              ncat tmux tmuxinator            
```

Client machines:
```
$ apt install sshfs openssh-sftp-server 
$ apt install tmux tmuxinator            # optional, only for nested sessions
```


## Setting up

- [ ] Figure out the IP addresses of all devices. Adjust them in `tmuxinator.yml` and `ssh.config`
- [ ] Specify the shared dir on the host in `ssh.config` (`sshfs localhost:$PATH ...`)
- [ ] Specify its mount path on clients in `ssh.config`. Ensure:
    - [ ] Path exists
    - [ ] Is a directory 
    - [ ] Is empty


## Quickstart

Run `./tmuxinator.yml` to start the parent tmux session that will get everything moving. The prefix key has been changed to ^A so that any client can use the default, see and modify the repo's `tmux.conf` file as you like.

Be very careful and mind the following:

- Mount point could be left unmounted, keep an eye on warnings if any
- Mount point is read/write for all clients
- Weird stuff can happen when layering `tmux`
- Do not put more than one finger in the power plug



