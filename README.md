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

From the provided boilerplate, adjust the `tmuxinator.yml` and `ssh.config` files to your liking. 

- Tune `tmuxinator.yml` to connect `tmux` panes to your devices: `ssh -F ssh.config user@192.168.21.28`
- Tune `ssh.config` to define networking behavior for each desired connection.
    - Ajust target IP addresses
    - Assign arbitrary unique ports to enable reverse-calling `sshfs`
    - Specify the shared dir on the host and its mount path on clients

On clients, ensure the mount path exists as an empty directory.

Find a `ssh.config` file overview for a single connection [here](.fig/ssh_config.png).


## Quickstart

Run `./tmuxinator.yml` to start the parent `tmux` session that will get everything moving. Its prefix key has been changed to `^A` so that any client can use the default, see and modify the repo's `tmux.conf` file as you like.

After you're logged in the remotes, try sweet commands like `ls` or `touch f` to verify that your files are indeed being shared.

Be very careful and mind the following:

- Mount point could be left unmounted, keep an eye on warnings if any
- Mount point is read/write for all clients
- Weird stuff can happen when layering `tmux`
- Do not put more than one finger in the power plug


