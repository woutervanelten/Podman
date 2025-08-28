# Usage
Containers (and pods) can have their own network. \
If a container needs to reach the host network, most of the time this will fail. \
 \
For instance, you want Traefik to reach a service (eg. Cockpit) on the LXC. \
Normally you'll put `- url: "https://***.***.***.***:9090` in it. But, this will fail in a Bad Gateway. \
 \
To fix this, podman has a special DNS host name to reach the host of podman. \
**host.containers.internal** \
So, putting `- url: "https://host.containers.internal:9090"` in traefik fixes this.

## systemd config.
in [Unit] \
Requires= This .pod or .container (service) tries to start the mentioned services if they are not already running. If the mentioned service is stopped or fails to start, this .pod or .service will not start, or will also stop. \
Wants= This .pod or .container (service) tries to start the mentioned services if they are not already running. If the mentioned service is stopped or fails to start, this .pod or .service will start nevertheless. \
After= This .pod or .container (service) is started after the mentioned services are started.
