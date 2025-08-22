# Installation steps to get podman rootless working.

> **Note**,
> This is still a work in progress.
> As long as this text is still here, everithing in this file is just a collection of notes that I use to create the howto eventually.

> **NOTE**,
> If a command needs to be run at the host, it is entered as @HOST: `code to run` \
> If it needs to be run at the container, it is entered als @CT: `code to run` \
> If you need to run it as root there is a "#" in front. \
> Example, \
> command to run as root on the container: @CT `# apt update` \
> command to run as user on the container: @CT `systemctl --user daemon-reload`

 \
 # Folders and files
 Create a working directory. @CT `mkdir -p ~/.config/containers/systemd` \
  \
 To allow services to start automatically, don't forget to run: \
`loginctl enable-linger USERNAME`
