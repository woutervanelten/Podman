# Installation steps to get podman rootless working.

> **Note**,
> This is still a work in progress.
> As long as this text is still here, everithing in this file is just a collection of notes that I use to create the howto eventually.

> **NOTE**,
> The host is the Proxmox system.
> The LXC is the LXC on Proxmox.
> The container is the pod/systemd container on the LXC.
> 
> If a command needs to be run at the host (Proxmox), it is entered as @HOST: `code to run` \
> If it needs to be run at the LXC, it is entered as `code to run` \
> If it needs to be run inside the container, it is entered as @POD: `code to run` \
> If you need to run it as root there is a "#" in front. \
> Example, \
> command to run as root on the host: @HOST `# apt update` \
> command to run as user on the container: `systemctl --user daemon-reload`


# Folders and files
Create a working directory. `mkdir -p ~/.config/containers/systemd` 
  
# Set permissions on folders
Files or folders on you CT that you want to access with the container should have the right user:owner permissions. \
For podman (and also the unprivileged LXC) there will be user and group mapping. \
This is done in /etc/subuid and /etc/subgid \
Mine are set username (check with whoami) :65536:65536. \
`podmanuser:65536:65536` \
This means that the user and group ID inside the container is increased with 65536 and that will be the user and group ID in the LXC. (So root in container (id 0 ) is id 65536 in the LXC, user 1000 in the container is user 66536 inside the LXC. \
To get the required user(s) from a pod, you can run: `podman top CONTAINERNAME user huser`

 
# Auto start of services
To allow services to start automatically, don't forget to run: \
`loginctl enable-linger $(whoami)`

# Test a pod before starting it
It is possible to check a service without starting it. \
You have 2 options for this:
`systemd-analyze --user --generators=true verify testthisone.service` \
or \
`/usr/lib/systemd/system-generators/podman-system-generator --user --dryrun > /dev/null`
