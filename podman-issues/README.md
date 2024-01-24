# Podman Issues

### ⚠️ Issue

Podman containers in production environment getting stopped automatically even in daemon mode.

### 🔍 Findings

1. Podman supports running containers in both rootful and rootless mode. This allows a container to run without having full access across the host system.
2. However, running a container in rootless mode restricts the user / container from having certain privileges, in our case the REST API UNIX socket.
3. While it is possible to provide these privileges to the user group, the recommended way is to setup a DOCKER_HOST environment variable that that will point to the user specific socket.
4. Apart from that, the linux system manager (systemd) could also kill a container once the user session is expired. To get rid of this, we need to enable lingering for the linux user.

### 🔧 Fix

For enabling the the user specific socket, run

```bash
systemctl --user enable podman.socket --now
```

Once done, we need to get the path to the specific socket by running,

```bash
podman info | grep -A2 'remoteSocket'
```

Now, edit the bash profile file to include the obtained path

```bash
vi ~/.bash_profile

# insert like the following line

export DOCKER_HOST=unix:///path/to/podman.sock
```

Save the file and source to apply the changes

```bash
source ~/.bash_profile
```

Finally, create / edit the _testcontainers.properties_ file present in the root directory

```bash
vi ~/.testcontainers.properties

# insert the following line

ryuk.container.privileged=true
```

Additionaly, if lingering is disabled by default, run the following command to enable it, thus we can restrict systemd from killing the container when the user log out.

```bash
loginctl enable-linger

# check lingering status

loginctl show-user user -p Linger
```

Now, restart the containers and it should work without fail.
