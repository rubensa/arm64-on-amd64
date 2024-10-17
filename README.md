# arm64-on-amd64

Minimal reproducible example for the Issue: [ptyHost was unable to resolve shell environment (arm64 container running on amd64 host)](https://github.com/microsoft/vscode-remote-release/issues/10396).

## Development

This repo is aimed to be opened in **[VSCode](https://code.visualstudio.com/)** with the **[Dev Containers](https://code.visualstudio.com/docs/devcontainers/containers)** extension installed on a **amd64** architecture Linux machine.

The development is done inside a **[Docker container](https://docker.com/)** architecture using an **arm64** [image](https://github.com/rubensa/docker-ubuntu-tini-dev) with multiple development tools already pre-installed.

Please, make sure you have **VSCode** with the **Dev Containers** extension and **Docker** installed and working on your system before cloning the respository.

You also need to enable running **arm64** containers on **amd64** host by running:

```bash
sudo apt-get install qemu binfmt-support qemu-user-static # Install the qemu packages
docker run --rm --privileged multiarch/qemu-user-static --reset -p yes # This step will execute the registering scripts
```

For more info on this, you can check [here](https://www.stereolabs.com/docs/docker/building-arm-container-on-x86).

Then clone the repository:

`git clone https://github.com/rubensa/arm64-on-amd64.git`

For detailed instructions see: **[Developing inside a Container](https://code.visualstudio.com/docs/remote/containers)**.

## Project Organization

    ├── .devcontainer     <- VSCode Remote Development configuration
    │
    └── README.md         <- This file

## Showing the issue

You should see the issue in **Dev Containers** log (F1 + _Dev Containers: Show Container Log_).

<details>
  <summary>Click to show log</summary>

```bash
[288 ms] Dev Containers 0.388.0 in VS Code 1.94.2 (384ff7382de624fb94dbaf6da11977bba1ecd427).
[285 ms] Start: Resolving Remote
[384 ms] Setting up container for folder or workspace: /work/arm64-on-amd64
[528 ms] Start: Check Docker is running
[531 ms] Start: Run: docker version
[617 ms] Client:
 Version:           24.0.7
 API version:       1.43
 Go version:        go1.20.10
 Git commit:        afdd53b
 Built:             Thu Oct 26 09:04:00 2023
 OS/Arch:           linux/amd64
[623 ms] 
 Context:           default

Server: Docker Engine - Community
 Engine:
  Version:          24.0.7
  API version:      1.43 (minimum version 1.12)
  Go version:       go1.20.10
  Git commit:       311b9ff
  Built:            Thu Oct 26 09:05:28 2023
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          v1.7.6
  GitCommit:        091922f03c2762540fd057fba91260237ff86acb
 runc:
  Version:          1.1.9
  GitCommit:        v1.1.9-0-gccaecfc
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
[638 ms] Start: Run: docker volume ls -q
[731 ms] Start: Run: docker inspect --type container 9714598e1e5543418e845424ed41b2e9cf5b2f491b74d85b2a0cba17a1d18253
[818 ms] Start: Run: docker ps -q -a --filter label=vsch.local.folder=/work/arm64-on-amd64 --filter label=vsch.quality=stable
[925 ms] Start: Run: docker ps -q -a --filter label=devcontainer.local_folder=/work/arm64-on-amd64 --filter label=devcontainer.config_file=/work/arm64-on-amd64/.devcontainer/devcontainer.json
[1034 ms] Start: Run: docker ps -q -a --filter label=devcontainer.local_folder=/work/arm64-on-amd64
[1126 ms] Start: Run: docker ps -q -a --filter label=devcontainer.local_folder=/work/arm64-on-amd64
[1195 ms] Running Dev Containers CLI:   up --user-data-folder /home/rubensa/.config/Code/User/globalStorage/ms-vscode-remote.remote-containers/data --container-session-data-folder /tmp/devcontainers-94cc2385-5836-4228-8643-2d9977ff4a5f1729171206082 --workspace-folder /work/arm64-on-amd64 --workspace-mount-consistency cached --gpu-availability detect --id-label devcontainer.local_folder=/work/arm64-on-amd64 --id-label devcontainer.config_file=/work/arm64-on-amd64/.devcontainer/devcontainer.json --log-level debug --log-format json --config /work/arm64-on-amd64/.devcontainer/devcontainer.json --default-user-env-probe loginInteractiveShell --build-no-cache --mount type=volume,source=vscode,target=/vscode,external=true --skip-post-create --update-remote-user-uid-default on --mount-workspace-git-root --include-configuration --include-merged-configuration
[1199 ms] Start: Run: /opt/VSCode-linux-x64-1.94.2/code /home/rubensa/.vscode/extensions/ms-vscode-remote.remote-containers-0.388.0/dist/spec-node/devContainersSpecCLI.js up --user-data-folder /home/rubensa/.config/Code/User/globalStorage/ms-vscode-remote.remote-containers/data --container-session-data-folder /tmp/devcontainers-94cc2385-5836-4228-8643-2d9977ff4a5f1729171206082 --workspace-folder /work/arm64-on-amd64 --workspace-mount-consistency cached --gpu-availability detect --id-label devcontainer.local_folder=/work/arm64-on-amd64 --id-label devcontainer.config_file=/work/arm64-on-amd64/.devcontainer/devcontainer.json --log-level debug --log-format json --config /work/arm64-on-amd64/.devcontainer/devcontainer.json --default-user-env-probe loginInteractiveShell --build-no-cache --mount type=volume,source=vscode,target=/vscode,external=true --skip-post-create --update-remote-user-uid-default on --mount-workspace-git-root --include-configuration --include-merged-configuration
[2425 ms] @devcontainers/cli 0.71.0. Node.js v20.16.0. linux 6.8.0-47-generic x64.
[2424 ms] Start: Run: docker buildx version
[2659 ms] github.com/docker/buildx v0.12.1 30feaa1a915b869ebc2eea6328624b49facd4bfb
[2659 ms] 
[2660 ms] Start: Run: docker -v
[2701 ms] Start: Resolving Remote
[2729 ms] Loading 146 extra certificates from /etc/ssl/certs/ca-certificates.crt.
[2903 ms] Start: Run: docker compose version --short
[3101 ms] Docker Compose version: 2.24.1
[3101 ms] Start: Run: docker compose -f /work/arm64-on-amd64/.devcontainer/docker-compose.yml --profile * config
[3304 ms] name: devcontainer
services:
  arm64-on-amd64:
    build:
      context: /work/arm64-on-amd64/.devcontainer
      dockerfile: Dockerfile
    networks:
      default: null
    platform: linux/arm64
    volumes:
      - type: bind
        source: /work/arm64-on-amd64
        target: /workspaces/arm64-on-amd64
networks:
  default:
    name: devcontainer_default
[3321 ms] Start: Run: docker ps -q -a --filter label=com.docker.compose.project=arm64-on-amd64_devcontainer --filter label=com.docker.compose.service=arm64-on-amd64
[3366 ms] Start: Run: docker events --format {{json .}} --filter event=start
[3378 ms] PersistedPath=/home/rubensa/.config/Code/User/globalStorage/ms-vscode-remote.remote-containers/data, ContainerHasLabels=false
[3381 ms] Start: Run: docker compose -f /work/arm64-on-amd64/.devcontainer/docker-compose.yml --profile * config
[3616 ms] name: devcontainer
services:
  arm64-on-amd64:
    build:
      context: /work/arm64-on-amd64/.devcontainer
      dockerfile: Dockerfile
    networks:
      default: null
    platform: linux/arm64
    volumes:
      - type: bind
        source: /work/arm64-on-amd64
        target: /workspaces/arm64-on-amd64
networks:
  default:
    name: devcontainer_default
[3627 ms] Start: Run: docker inspect --type image rubensa/ubuntu-tini-dev
[4097 ms] Start: Run: docker-credential-secretservice get
[6434 ms] Docker Compose override file for building image:
services:
  arm64-on-amd64:
    build:
      dockerfile: /tmp/devcontainercli-rubensa/container-features/0.71.0-1729171215903/Dockerfile-with-features
      args:
        - BUILDKIT_INLINE_CACHE=1
        - _DEV_CONTAINERS_BASE_IMAGE=dev_container_auto_added_stage_label

[6435 ms] Start: Run: docker compose --project-name arm64-on-amd64_devcontainer -f /work/arm64-on-amd64/.devcontainer/docker-compose.yml -f /home/rubensa/.config/Code/User/globalStorage/ms-vscode-remote.remote-containers/data/docker-compose/docker-compose.devcontainer.build-1729171215905.yml build --no-cache
#0 building with "default" instance using docker driver

#1 [arm64-on-amd64 internal] load build definition from Dockerfile-with-features
#1 transferring dockerfile: 623B done
#1 DONE 0.0s

#2 [arm64-on-amd64 internal] load .dockerignore
#2 transferring context: 2B done
#2 DONE 0.0s

#3 [arm64-on-amd64] resolve image config for docker.io/docker/dockerfile:1.4
#3 ...

#4 [arm64-on-amd64 auth] docker/dockerfile:pull token for registry-1.docker.io
#4 DONE 0.0s

#3 [arm64-on-amd64] resolve image config for docker.io/docker/dockerfile:1.4
#3 DONE 1.0s

#5 [arm64-on-amd64] docker-image://docker.io/docker/dockerfile:1.4@sha256:9ba7531bd80fb0a858632727cf7a112fbfd19b17e94c4e84ced81e24ef1a0dbc
#5 CACHED

#6 [arm64-on-amd64 internal] load metadata for docker.io/rubensa/ubuntu-tini-dev:latest
#6 ...

#7 [arm64-on-amd64 auth] rubensa/ubuntu-tini-dev:pull token for registry-1.docker.io
#7 DONE 0.0s

#6 [arm64-on-amd64 internal] load metadata for docker.io/rubensa/ubuntu-tini-dev:latest
#6 DONE 0.8s

#8 [arm64-on-amd64 dev_container_auto_added_stage_label 1/1] FROM docker.io/rubensa/ubuntu-tini-dev@sha256:0d7414c6de7396581ad2bc699f4407dd337fa79133b6d9ba9a8f05680b8362ca
#8 CACHED

#9 [arm64-on-amd64] preparing layers for inline cache
#9 DONE 0.0s

#10 [arm64-on-amd64] exporting to image
#10 exporting layers done
#10 writing image sha256:a17acfea3125b663aa1c75d3a3ed688f4b3c87453e73934673651f242dd1bb25 done
#10 naming to docker.io/library/arm64-on-amd64_devcontainer-arm64-on-amd64 0.0s done
#10 DONE 0.0s
[8840 ms] Start: Run: docker inspect --type image arm64-on-amd64_devcontainer-arm64-on-amd64
[8856 ms] Start: Run: docker build -f /tmp/devcontainercli-rubensa/updateUID.Dockerfile-0.71.0 -t vsc-arm64-on-amd64-f60d13b33f6a73aa103fd6c2f820fe75f3ca14d9d2bc72f902324bfbe0691612-uid --platform linux/arm64 --build-arg BASE_IMAGE=arm64-on-amd64_devcontainer-arm64-on-amd64 --build-arg REMOTE_USER=user --build-arg NEW_UID=1000 --build-arg NEW_GID=1000 --build-arg IMAGE_USER=user /home/rubensa/.config/Code/User/globalStorage/ms-vscode-remote.remote-containers/data/empty-folder
#0 building with "default" instance using docker driver

#1 [internal] load build definition from updateUID.Dockerfile-0.71.0
#1 transferring dockerfile: 1.36kB done
#1 DONE 0.0s

#2 [internal] load .dockerignore
#2 transferring context: 2B done
#2 DONE 0.0s

#3 [internal] load metadata for docker.io/library/arm64-on-amd64_devcontainer-arm64-on-amd64:latest
#3 DONE 0.0s

#4 [1/2] FROM docker.io/library/arm64-on-amd64_devcontainer-arm64-on-amd64
#4 DONE 0.0s

#5 [2/2] RUN eval $(sed -n "s/user:[^:]*:\([^:]*\):\([^:]*\):[^:]*:\([^:]*\).*/OLD_UID=\1;OLD_GID=\2;HOME_FOLDER=\3/p" /etc/passwd);    eval $(sed -n "s/\([^:]*\):[^:]*:1000:.*/EXISTING_USER=\1/p" /etc/passwd);         eval $(sed -n "s/\([^:]*\):[^:]*:1000:.*/EXISTING_GROUP=\1/p" /etc/group);      if [ -z "$OLD_UID" ]; then              echo "Remote user not found in /etc/passwd (user).";       elif [ "$OLD_UID" = "1000" -a "$OLD_GID" = "1000" ]; then               echo "UIDs and GIDs are the same (1000:1000).";         elif [ "$OLD_UID" != "1000" -a -n "$EXISTING_USER" ]; then echo "User with UID exists ($EXISTING_USER=1000).";     else            if [ "$OLD_GID" != "1000" -a -n "$EXISTING_GROUP" ]; then                       echo "Group with GID exists ($EXISTING_GROUP=1000).";                      NEW_GID="$OLD_GID";             fi;             echo "Updating UID:GID from $OLD_UID:$OLD_GID to 1000:1000.";           sed -i -e "s/\(user:[^:]*:\)[^:]*:[^:]*/\11000:1000/" /etc/passwd;                 if [ "$OLD_GID" != "1000" ]; then                       sed -i -e "s/\([^:]*:[^:]*:\)${OLD_GID}:/\11000:/" /etc/group;          fi;             chown -R 1000:1000 $HOME_FOLDER;   fi;
#5 CACHED

#6 exporting to image
#6 exporting layers done
#6 writing image sha256:17aca189035627f353b4654838bdccd9b05b30c4db7260a89e59c68851eed5ab done
#6 naming to docker.io/library/vsc-arm64-on-amd64-f60d13b33f6a73aa103fd6c2f820fe75f3ca14d9d2bc72f902324bfbe0691612-uid 0.0s done
#6 DONE 0.0s
[9198 ms] Docker Compose override file for creating container:
services:
  'arm64-on-amd64':
    image: vsc-arm64-on-amd64-f60d13b33f6a73aa103fd6c2f820fe75f3ca14d9d2bc72f902324bfbe0691612-uid
    entrypoint: ["/bin/sh", "-c", "echo Container started\n
trap \"exit 0\" 15\n
\n
exec \"$$@\"\n
while sleep 1 & wait $$!; do :; done", "-"]
    command: []
    labels:
      - 'devcontainer.local_folder=/work/arm64-on-amd64'
      - 'devcontainer.config_file=/work/arm64-on-amd64/.devcontainer/devcontainer.json'
    volumes:
      - vscode:/vscode
volumes:
  
  vscode:
    external: true
[9198 ms] Writing docker-compose.devcontainer.containerFeatures-1729171218669-5e1d07b2-9958-425b-a525-cfc80dea28e7.yml to /home/rubensa/.config/Code/User/globalStorage/ms-vscode-remote.remote-containers/data/docker-compose
[9199 ms] Start: Run: docker compose --project-name arm64-on-amd64_devcontainer -f /work/arm64-on-amd64/.devcontainer/docker-compose.yml -f /home/rubensa/.config/Code/User/globalStorage/ms-vscode-remote.remote-containers/data/docker-compose/docker-compose.devcontainer.build-1729171215905.yml -f /home/rubensa/.config/Code/User/globalStorage/ms-vscode-remote.remote-containers/data/docker-compose/docker-compose.devcontainer.containerFeatures-1729171218669-5e1d07b2-9958-425b-a525-cfc80dea28e7.yml up -d
[+] Running 1/1
 ✔ Container arm64-on-amd64_devcontainer-arm64-on-amd64-1  Started         0.4s 
[9657 ms] Start: Run: docker ps -q -a --filter label=com.docker.compose.project=arm64-on-amd64_devcontainer --filter label=com.docker.compose.service=arm64-on-amd64
[9680 ms] Start: Run: docker inspect --type container 03c207d674a5
[9699 ms] Start: Inspecting container
[9699 ms] Start: Run: docker inspect --type container 03c207d674a50303ebea84e44db0a7185a83610d707d2b48778b9f6852cd1134
[9723 ms] Start: Run in container: /bin/sh
[9727 ms] Start: Run in container: uname -m
[9878 ms] aarch64
[9878 ms] 
[9878 ms] Start: Run in container: (cat /etc/os-release || cat /usr/lib/os-release) 2>/dev/null
[9928 ms] PRETTY_NAME="Ubuntu 24.04.1 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.1 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo
[9928 ms] 
[9929 ms] Start: Run in container:  (command -v getent >/dev/null 2>&1 && getent passwd 'user' || grep -E '^user|^[^:]*:[^:]*:user:' /etc/passwd || true)
[9988 ms] Start: Run in container: test -f '/var/devcontainer/.patchEtcEnvironmentMarker'
[9992 ms] 
[9993 ms] 
[9993 ms] Exit code 1
[9993 ms] Start: Run in container: /bin/sh
[9998 ms] Start: Run in container: test ! -f '/var/devcontainer/.patchEtcEnvironmentMarker' && set -o noclobber && mkdir -p '/var/devcontainer' && { > '/var/devcontainer/.patchEtcEnvironmentMarker' ; } 2> /dev/null
[10141 ms] 
[10141 ms] 
[10141 ms] Start: Run in container: cat >> /etc/environment <<'etcEnvrionmentEOF'
[10192 ms] 
[10192 ms] 
[10193 ms] Start: Run in container: test -f '/var/devcontainer/.patchEtcProfileMarker'
[10197 ms] 
[10197 ms] 
[10197 ms] Exit code 1
[10197 ms] Start: Run in container: test ! -f '/var/devcontainer/.patchEtcProfileMarker' && set -o noclobber && mkdir -p '/var/devcontainer' && { > '/var/devcontainer/.patchEtcProfileMarker' ; } 2> /dev/null
[10243 ms] 
[10243 ms] 
[10243 ms] Start: Run in container: sed -i -E 's/((^|\s)PATH=)([^\$]*)$/\1${PATH:-\3}/g' /etc/profile || true
[10330 ms] 
[10330 ms] 
[10339 ms] Start: Run: docker inspect --type container 03c207d674a50303ebea84e44db0a7185a83610d707d2b48778b9f6852cd1134
[10359 ms] Start: Run: docker exec -i -u root 03c207d674a50303ebea84e44db0a7185a83610d707d2b48778b9f6852cd1134 /bin/sh -c echo "New container started. Keep-alive process started." ; export VSCODE_REMOTE_CONTAINERS_SESSION=94cc2385-5836-4228-8643-2d9977ff4a5f1729171206082 ; /bin/sh
[10369 ms] Start: Inspecting container
[10369 ms] Start: Run: docker inspect --type container 03c207d674a50303ebea84e44db0a7185a83610d707d2b48778b9f6852cd1134
[10395 ms] Start: Run in container: /bin/sh
[10407 ms] Start: Run in container: uname -m
[10465 ms] New container started. Keep-alive process started.
[10551 ms] aarch64
[10552 ms] 
[10552 ms] Start: Run in container: (cat /etc/os-release || cat /usr/lib/os-release) 2>/dev/null
[10594 ms] PRETTY_NAME="Ubuntu 24.04.1 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.1 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo
[10594 ms] 
[10594 ms] Start: Run in container:  (command -v getent >/dev/null 2>&1 && getent passwd 'user' || grep -E '^user|^[^:]*:[^:]*:user:' /etc/passwd || true)
[10656 ms] Start: Run in container: command -v git >/dev/null 2>&1 && ROOT_FOLDER="$(git -C '/workspaces/arm64-on-amd64' rev-parse --show-toplevel)" && test "$(stat -c %u "$ROOT_FOLDER")" != "$(id -u)" && echo -n "$ROOT_FOLDER"
[10721 ms] 
[10721 ms] fatal: not a git repository (or any parent up to mount point /workspaces)
Stopping at filesystem boundary (GIT_DISCOVERY_ACROSS_FILESYSTEM not set).
[10721 ms] Exit code 128
[10722 ms] Start: Updating configuration state
[10728 ms] Start: Run: docker compose version --short
[10803 ms] Docker Compose version: 2.24.1
[10804 ms] Start: Setup shutdown monitor
[10805 ms] Forking shutdown monitor: /home/rubensa/.vscode/extensions/ms-vscode-remote.remote-containers-0.388.0/dist/shutdown/shutdownMonitorProcess /run/user/1000/vscode-remote-containers-5b1e669b-9b32-4384-bd50-78b7b080e3d1.sock dockerCompose Debug /home/rubensa/.config/Code/logs/20241017T070239/window6/exthost/ms-vscode-remote.remote-containers 1729171209471
[10813 ms] Start: Run in container: test -d '/home/user/.vscode-server'
[10818 ms] 
[10818 ms] 
[10818 ms] Exit code 1
[10818 ms] Start: Run in container: test -d '/home/user/.vscode-remote'
[10824 ms] 
[10824 ms] 
[10824 ms] Exit code 1
[10825 ms] Start: Run in container: test ! -f '/home/user/.vscode-server/data/Machine/.writeMachineSettingsMarker' && set -o noclobber && mkdir -p '/home/user/.vscode-server/data/Machine' && { > '/home/user/.vscode-server/data/Machine/.writeMachineSettingsMarker' ; } 2> /dev/null
[10884 ms] 
[10885 ms] 
[10885 ms] Start: Run in container: mkdir -p '/home/user/.vscode-server/data/Machine' && cat >'/home/user/.vscode-server/data/Machine/settings.json' <<'settingsJSON'
[10971 ms] 
[10972 ms] 
[10973 ms] 
Support for ARM64 is in preview.

[10973 ms] Start: Run in container: test -d '/home/user/.vscode-server/bin/384ff7382de624fb94dbaf6da11977bba1ecd427'
[10978 ms] 
[10979 ms] 
[10979 ms] Exit code 1
[10979 ms] Start: Run in container: test -d '/vscode/vscode-server/bin/linux-arm64/384ff7382de624fb94dbaf6da11977bba1ecd427'
[10985 ms] 
[10985 ms] 
[10986 ms] Start: Run in container: mkdir -p '/home/user/.vscode-server/bin' && ln -snf '/vscode/vscode-server/bin/linux-arm64/384ff7382de624fb94dbaf6da11977bba1ecd427' '/home/user/.vscode-server/bin/384ff7382de624fb94dbaf6da11977bba1ecd427'
[11071 ms] 
[11071 ms] 
[11071 ms] Start: Run in container: /bin/sh
[11076 ms] Start: Run in container: test -x '/home/user/.vscode-server/bin/384ff7382de624fb94dbaf6da11977bba1ecd427/bin/helpers/check-requirements.sh'
[11077 ms] Start: Run in container: touch '/vscode/vscode-server/bin/linux-arm64/384ff7382de624fb94dbaf6da11977bba1ecd427'
[11082 ms] 
[11082 ms] 
[11082 ms] Start: Run in container: '/home/user/.vscode-server/bin/384ff7382de624fb94dbaf6da11977bba1ecd427/bin/helpers/check-requirements.sh'
[11231 ms] 
[11231 ms] 
[12519 ms] 
[12519 ms] 
[12520 ms] Start: Launching Dev Containers helper.
[12520 ms] ssh-agent: SSH_AUTH_SOCK in container (/tmp/vscode-ssh-auth-3139d431-eb95-43bc-8531-e08c78060fe9.sock) forwarded to local host (/run/user/1000/keyring/ssh).
[12521 ms] Start: Run in container: test -e /tmp/.X11-unix/X0
[12525 ms] 
[12525 ms] 
[12525 ms] Exit code 1
[12526 ms] Start: Run in container: mkdir -p '/tmp/.X11-unix'
[12562 ms] 
[12562 ms] 
[12562 ms] X11 forwarding: DISPLAY in container (:0) forwarded to local host (:0).
[12563 ms] Start: Run in container: gpgconf --list-dirs
[12609 ms] sysconfdir:/etc/gnupg
bindir:/usr/bin
libexecdir:/usr/lib/gnupg
libdir:/usr/lib/aarch64-linux-gnu/gnupg
datadir:/usr/share/gnupg
localedir:/usr/share/locale
socketdir:/home/user/.gnupg
dirmngr-socket:/home/user/.gnupg/S.dirmngr
keyboxd-socket:/home/user/.gnupg/S.keyboxd
agent-ssh-socket:/home/user/.gnupg/S.gpg-agent.ssh
agent-extra-socket:/home/user/.gnupg/S.gpg-agent.extra
agent-browser-socket:/home/user/.gnupg/S.gpg-agent.browser
agent-socket:/home/user/.gnupg/S.gpg-agent
homedir:/home/user/.gnupg
[12609 ms] 
[12610 ms] Start: Run in container: ls '/home/user/.gnupg/private-keys-v1.d' 2>/dev/null
[12661 ms] 
[12661 ms] 
[12661 ms] Exit code 2
[12662 ms] Start: Run in container: grep -e '^s*use-keyboxds*$' '/home/user/.gnupg/common.conf' 2>/dev/null
[12729 ms] 
[12729 ms] 
[12729 ms] Exit code 2
[12730 ms] Start: Run: gpgconf --list-dirs
[12746 ms] sysconfdir:/etc/gnupg
bindir:/usr/bin
libexecdir:/usr/lib/gnupg
libdir:/usr/lib/x86_64-linux-gnu/gnupg
datadir:/usr/share/gnupg
localedir:/usr/share/locale
socketdir:/run/user/1000/gnupg
dirmngr-socket:/run/user/1000/gnupg/S.dirmngr
agent-ssh-socket:/run/user/1000/gnupg/S.gpg-agent.ssh
agent-extra-socket:/run/user/1000/gnupg/S.gpg-agent.extra
agent-browser-socket:/run/user/1000/gnupg/S.gpg-agent.browser
agent-socket:/run/user/1000/gnupg/S.gpg-agent
homedir:/home/rubensa/.gnupg
[12746 ms] 
[12746 ms] Start: Run in container: test -f '/home/user/.gnupg/pubring.kbx'
[12752 ms] 
[12752 ms] 
[12752 ms] Exit code 1
[12752 ms] Start: Run in container: test -f '/home/user/.gnupg/pubring.gpg'
[12758 ms] 
[12759 ms] 
[12759 ms] Exit code 1
[12759 ms] Start: Run in container: test -f '/home/user/.gnupg/trustdb.gpg'
[12763 ms] 
[12764 ms] 
[12764 ms] Exit code 1
[12764 ms] Start: Run in container: mkdir -p -m 700 '/home/user/.gnupg'
[12764 ms] gpg-agent: Socket in container (/home/user/.gnupg/S.gpg-agent) forwarded to local host (/run/user/1000/gnupg/S.gpg-agent.extra).
[12805 ms] 
[12805 ms] 
[12805 ms] Start: Run in container: command -v docker >/dev/null 2>&1
[12810 ms] 
[12810 ms] 
[12810 ms] Start: Run in container: # Test for /home/user/.gnupg/pubring.kbx and gpg
[12811 ms] Start: Run in container: /bin/sh
[12818 ms] userEnvProbe: none
[12819 ms] Start: Run in container: echo ~
[12872 ms] 
[12872 ms] 
[12873 ms] Start: Run in container: # Test for /home/user/.ssh/known_hosts and ssh
[12937 ms] 
[12938 ms] 
[12939 ms] Start: Run in container: # Copy /home/rubensa/.gnupg/pubring.kbx to /home/user/.gnupg/pubring.kbx
[12954 ms] /home/user
[12954 ms] 
[12955 ms] Start: Run in container: cat <<'EOF-/tmp/vscode-remote-containers-3139d431-eb95-43bc-8531-e08c78060fe9.js' >/tmp/vscode-remote-containers-3139d431-eb95-43bc-8531-e08c78060fe9.js
[12997 ms] 
[12998 ms] 
[13001 ms] Start: Run in container: cat ~/.docker/config.json || echo "{
[13056 ms] {
}
[13056 ms] cat: /home/user/.docker/config.json: No such file or directory
[13056 ms] Start: Run in container: mkdir -p /usr/local/bin && cat <<'EOF-/usr/local/bin/docker-credential-dev-containers-3139d431-eb95-43bc-8531-e08c78060fe9' >/usr/local/bin/docker-credential-dev-containers-3139d431-eb95-43bc-8531-e08c78060fe9
[13065 ms] 
[13066 ms] 
[13067 ms] Start: Run in container: # Copy /home/rubensa/.ssh/known_hosts to /home/user/.ssh/known_hosts
[13152 ms] 
[13152 ms] 
[13152 ms] Start: Run in container: chmod +x /usr/local/bin/docker-credential-dev-containers-3139d431-eb95-43bc-8531-e08c78060fe9
[13191 ms] 
[13191 ms] 
[13193 ms] Start: Run in container: mkdir -p ~/.docker && cat <<'EOF-/usr/local/bin/docker-credential-dev-containers-3139d431-eb95-43bc-8531-e08c78060fe9' >~/.docker/config.json
[13193 ms] 
[13193 ms] 
[13193 ms] Start: Run in container: # Test for /home/user/.gnupg/trustdb.gpg and gpg
[13193 ms] Start: Run in container: command -v git >/dev/null 2>&1 && git config --system --replace-all credential.helper '!f() { /home/user/.vscode-server/bin/384ff7382de624fb94dbaf6da11977bba1ecd427/node /tmp/vscode-remote-containers-3139d431-eb95-43bc-8531-e08c78060fe9.js git-credential-helper $*; }; f' || true
[13247 ms] 
[13247 ms] 
[13247 ms] Start: Run in container: # Copy /home/rubensa/.gnupg/trustdb.gpg to /home/user/.gnupg/trustdb.gpg
[13289 ms] 
[13289 ms] 
[13293 ms] 
[13293 ms] 
[13293 ms] Start: Run in container: cat <<'EOF-/tmp/vscode-remote-containers-server-3139d431-eb95-43bc-8531-e08c78060fe9.js' >/tmp/vscode-remote-containers-server-3139d431-eb95-43bc-8531-e08c78060fe9.js_1729171222764
[13372 ms] 
[13372 ms] 
[13372 ms] Start: Run in container: for pid in `cd /proc && ls -d [0-9]*`; do { echo $pid ; readlink /proc/$pid/cwd || echo ; readlink /proc/$pid/ns/mnt || echo ; cat /proc/$pid/stat | tr "
[13373 ms] Start: Run: gpg-connect-agent updatestartuptty /bye
[13471 ms] 
[13472 ms] 
[15428 ms] Start: Run in container: cat '/home/user/.vscode-server/bin/384ff7382de624fb94dbaf6da11977bba1ecd427/product.json'
[15479 ms] Start: Run in container: cat '/home/user/.vscode-server/data/Machine/.connection-token-384ff7382de624fb94dbaf6da11977bba1ecd427' 2>/dev/null || (umask 377 && echo 'cf6ea50d-4351-4507-a5fb-3a3d223a148d' >'/home/user/.vscode-server/data/Machine/.connection-token-384ff7382de624fb94dbaf6da11977bba1ecd427-82c8ce25-212d-448a-8c2b-bd4a8a6a09a3' && mv -n '/home/user/.vscode-server/data/Machine/.connection-token-384ff7382de624fb94dbaf6da11977bba1ecd427-82c8ce25-212d-448a-8c2b-bd4a8a6a09a3' '/home/user/.vscode-server/data/Machine/.connection-token-384ff7382de624fb94dbaf6da11977bba1ecd427' && rm -f '/home/user/.vscode-server/data/Machine/.connection-token-384ff7382de624fb94dbaf6da11977bba1ecd427-82c8ce25-212d-448a-8c2b-bd4a8a6a09a3' && cat '/home/user/.vscode-server/data/Machine/.connection-token-384ff7382de624fb94dbaf6da11977bba1ecd427')
[15627 ms] cf6ea50d-4351-4507-a5fb-3a3d223a148d
[15628 ms] 
[15628 ms] Start: Starting VS Code Server
[15629 ms] Start: Preparing Extensions
[15629 ms] Start: Run in container: test ! -f '/home/user/.vscode-server/data/Machine/.installExtensionsMarker' && set -o noclobber && mkdir -p '/home/user/.vscode-server/data/Machine' && { > '/home/user/.vscode-server/data/Machine/.installExtensionsMarker' ; } 2> /dev/null
[15673 ms] 
[15673 ms] 
[15675 ms] Extensions cache, install extensions: GitHub.vscode-pull-request-github
[15675 ms] Start: Run in container: test -d /home/user/.vscode-server/extensionsCache && ls /home/user/.vscode-server/extensionsCache || true
[15682 ms] 
[15683 ms] 
[15683 ms] Start: Run in container: test -d /vscode/vscode-server/extensionsCache && ls /vscode/vscode-server/extensionsCache || true
[15745 ms] 42crunch.vscode-openapi-4.28.1
amodio.tsl-problem-matcher-0.6.2
atlassian.atlascode-3.0.10
circleci.circleci-2.8.4
codeium.codeium-1.14.12
dbaeumer.vscode-eslint-3.0.10
dgileadi.java-decompiler-0.0.4
dorzey.vscode-sqlfluff-3.1.4
dorzey.vscode-sqlfluff-3.2.0
eamodio.gitlens-15.2.0
eamodio.gitlens-15.2.1
eamodio.gitlens-15.2.3
eamodio.gitlens-15.3.1
eamodio.gitlens-15.4.0
eamodio.gitlens-15.5.0
eamodio.gitlens-15.5.1
eamodio.gitlens-15.6.0
eamodio.gitlens-15.6.1
esbenp.prettier-vscode-11.0.0
github.copilot-1.228.0
github.vscode-pull-request-github-0.94.0
github.vscode-pull-request-github-0.96.0
github.vscode-pull-request-github-0.98.0
humao.rest-client-0.25.1
irongeek.vscode-env-0.1.0
joyceerhl.github-graphql-nb-0.2.0
joyceerhl.vscode-graphql-notebook-0.2.0
madhavd1.javadoc-tools-1.6.0
mhutchie.git-graph-1.30.0
moshfeu.compare-folders-0.24.3
ms-azuretools.vscode-docker-1.29.1
ms-azuretools.vscode-docker-1.29.2
ms-kubernetes-tools.vscode-kubernetes-tools-1.3.16
ms-vscode.vscode-github-issue-notebooks-0.0.130
redhat.fabric8-analytics-0.9.5
redhat.java-1.34.0-linux-x64
ryu1kn.partial-diff-1.4.3
snowflake.snowflake-vsc-1.9.1
spring-javaformat-vscode-extension-0.0.35
visualstudioexptteam.vscodeintellicode-1.3.1
vivaxy.vscode-conventional-commits-1.26.0
vmware.vscode-boot-dev-pack-0.2.1
vmware.vscode-spring-boot-1.56.0
vscjava.vscode-gradle-3.16.4
vscjava.vscode-java-debug-0.58.0
vscjava.vscode-java-pack-0.29.0
vscjava.vscode-maven-0.44.0
vscjava.vscode-spring-boot-dashboard-0.14.0
vscjava.vscode-spring-initializr-0.11.2
[15745 ms] 
[15746 ms] Extensions cache, link in container: github.vscode-pull-request-github-0.94.0, github.vscode-pull-request-github-0.96.0, github.vscode-pull-request-github-0.98.0
[15746 ms] Start: Run in container: mkdir -p '/home/user/.vscode-server/extensionsCache' && ln -s '/vscode/vscode-server/extensionsCache'/* '/home/user/.vscode-server/extensionsCache' || true
[15826 ms] 
[15827 ms] 
[15827 ms] Optimizing extensions for quality: stable
[15827 ms] Start: Run in container: cd /vscode/vscode-server/extensionsCache && touch 'github.vscode-pull-request-github-0.94.0' 'github.vscode-pull-request-github-0.96.0' 'github.vscode-pull-request-github-0.98.0'
[15828 ms] Start: Run in container: /home/user/.vscode-server/bin/384ff7382de624fb94dbaf6da11977bba1ecd427/bin/code-server --log debug --force-disable-user-env --server-data-dir /home/user/.vscode-server --use-host-proxy --telemetry-level all --accept-server-license-terms --host 127.0.0.1 --port 0 --connection-token-file /home/user/.vscode-server/data/Machine/.connection-token-384ff7382de624fb94dbaf6da11977bba1ecd427 --extensions-download-dir /home/user/.vscode-server/extensionsCache --install-extension GitHub.vscode-pull-request-github --start-server --disable-websocket-compression --skip-requirements-check
[15879 ms] 
[15880 ms] 
[17905 ms] *
* Visual Studio Code Server
*
* By using the software, you agree to
* the Visual Studio Code Server License Terms (https://aka.ms/vscode-server-license) and
* the Microsoft Privacy Statement (https://privacy.microsoft.com/en-US/privacystatement).
*
[17982 ms] Server bound to 127.0.0.1:36975 (IPv4)
Extension host agent listening on 36975

[17983 ms] Start: Run in container: echo 36975 >'/home/user/.vscode-server/data/Machine/.devport-384ff7382de624fb94dbaf6da11977bba1ecd427'
[17988 ms] 
[17989 ms] 
[17989 ms] Port forwarding for container port 36975 starts listening on local port.
[17990 ms] Port forwarding local port 36975 to container port 36975
[17997 ms] Initializing configuration support...
[17997 ms] Internal initialization of dev container support package...
[18001 ms] Port forwarding connection from 51784 > 36975 > 36975 in the container.
[18002 ms] Start: Run in container: /home/user/.vscode-server/bin/384ff7382de624fb94dbaf6da11977bba1ecd427/node -e 
[18016 ms] Start: Run in container: # Test for /home/user/.gitconfig and git
[18076 ms] 
[18076 ms] 
[18077 ms] Start: Run in container: # Copy /home/rubensa/.gitconfig to /home/user/.gitconfig
[18210 ms] 
[18211 ms] 
[18212 ms] Start: Run in container: # Cleaning up git config
[18740 ms] 
[18740 ms] 
[18741 ms] Start: Run: git config --global --get gpg.ssh.allowedSignersFile
[18751 ms] Start: Run in container: command -v git >/dev/null 2>&1 && git config --global --replace-all credential.helper '!f() { /home/user/.vscode-server/bin/384ff7382de624fb94dbaf6da11977bba1ecd427/node /tmp/vscode-remote-containers-3139d431-eb95-43bc-8531-e08c78060fe9.js git-credential-helper $*; }; f' || true
[18760 ms] Copying allowed signers file: /home/rubensa/.ssh/allowed_signers
[18877 ms] 
[18878 ms] 
[18878 ms] Start: Run in container: # Test for /home/user/.ssh/allowed_signers and ssh
[18976 ms] 
[18976 ms] 
[18976 ms] Start: Run in container: # Copy /home/rubensa/.ssh/allowed_signers to /home/user/.ssh/allowed_signers
[19129 ms] 
[19129 ms] 
[19129 ms] Start: Run in container: git config --global gpg.ssh.allowedSignersFile '/home/user/.ssh/allowed_signers'
[19256 ms] 
[19256 ms] 
[19733 ms] Ignoring option 'skip-requirements-check': not supported for server.
[19922 ms] [13:20:29] 




[19938 ms] Port forwarding 51784 > 36975 > 36975 stderr: Connection established
[21113 ms] [13:20:30] Installing extensions...
[21150 ms] [13:20:30] Extension host agent started.
[21236 ms] Port forwarding connection from 56464 > 36975 > 36975 in the container.
[21237 ms] Start: Run in container: /home/user/.vscode-server/bin/384ff7382de624fb94dbaf6da11977bba1ecd427/node -e 
[21964 ms] [13:20:31] [127.0.0.1][8b65830c][ManagementConnection] New connection established.
[21989 ms] [13:20:31] Error while reading the extension cache file: /home/user/.vscode-server/data/CachedProfilesData/__default__profile__/extensions.builtin.cache Unable to read file '/home/user/.vscode-server/data/CachedProfilesData/__default__profile__/extensions.builtin.cache' (Error: Unable to resolve nonexistent file '/home/user/.vscode-server/data/CachedProfilesData/__default__profile__/extensions.builtin.cache')
[22025 ms] [13:20:31] Started initializing default profile extensions in extensions installation folder. file:///home/user/.vscode-server/extensions
[22491 ms] [13:20:31] Log level changed to info
[22592 ms] Port forwarding 56464 > 36975 > 36975 stderr: Connection established
[25409 ms] [13:20:34] [127.0.0.1][3d3b4d33][ExtensionHostConnection] New connection established.
[25679 ms] [13:20:35] [127.0.0.1][3d3b4d33][ExtensionHostConnection] <851> Launched Extension Host Process.
[28496 ms] [13:20:37] Completed initializing default profile extensions in extensions installation folder. file:///home/user/.vscode-server/extensions
[33916 ms] [13:20:43] ptyHost was unable to resolve shell environment Error: Unable to resolve your shell environment in a reasonable time. Please review your shell configuration and restart.
    at Timeout.<anonymous> (file:///vscode/vscode-server/bin/linux-arm64/384ff7382de624fb94dbaf6da11977bba1ecd427/out/vs/server/node/server.main.js:48:731)
    at listOnTimeout (node:internal/timers:581:17)
    at process.processTimers (node:internal/timers:519:7)
[33920 ms] [13:20:43] ptyHost was unable to resolve shell environment Error: Unable to resolve your shell environment in a reasonable time. Please review your shell configuration and restart.
    at Timeout.<anonymous> (file:///vscode/vscode-server/bin/linux-arm64/384ff7382de624fb94dbaf6da11977bba1ecd427/out/vs/server/node/server.main.js:48:731)
    at listOnTimeout (node:internal/timers:581:17)
    at process.processTimers (node:internal/timers:519:7)
[33923 ms] [13:20:43] ptyHost was unable to resolve shell environment Error: Unable to resolve your shell environment in a reasonable time. Please review your shell configuration and restart.
    at Timeout.<anonymous> (file:///vscode/vscode-server/bin/linux-arm64/384ff7382de624fb94dbaf6da11977bba1ecd427/out/vs/server/node/server.main.js:48:731)
    at listOnTimeout (node:internal/timers:581:17)
    at process.processTimers (node:internal/timers:519:7)
[33924 ms] [13:20:43] ptyHost was unable to resolve shell environment Error: Unable to resolve your shell environment in a reasonable time. Please review your shell configuration and restart.
    at Timeout.<anonymous> (file:///vscode/vscode-server/bin/linux-arm64/384ff7382de624fb94dbaf6da11977bba1ecd427/out/vs/server/node/server.main.js:48:731)
    at listOnTimeout (node:internal/timers:581:17)
    at process.processTimers (node:internal/timers:519:7)
[33928 ms] [13:20:43] ptyHost was unable to resolve shell environment Error: Unable to resolve your shell environment in a reasonable time. Please review your shell configuration and restart.
    at Timeout.<anonymous> (file:///vscode/vscode-server/bin/linux-arm64/384ff7382de624fb94dbaf6da11977bba1ecd427/out/vs/server/node/server.main.js:48:731)
    at listOnTimeout (node:internal/timers:581:17)
    at process.processTimers (node:internal/timers:519:7)
[33930 ms] [13:20:43] ptyHost was unable to resolve shell environment Error: Unable to resolve your shell environment in a reasonable time. Please review your shell configuration and restart.
    at Timeout.<anonymous> (file:///vscode/vscode-server/bin/linux-arm64/384ff7382de624fb94dbaf6da11977bba1ecd427/out/vs/server/node/server.main.js:48:731)
    at listOnTimeout (node:internal/timers:581:17)
    at process.processTimers (node:internal/timers:519:7)
[33934 ms] [13:20:43] ptyHost was unable to resolve shell environment Error: Unable to resolve your shell environment in a reasonable time. Please review your shell configuration and restart.
    at Timeout.<anonymous> (file:///vscode/vscode-server/bin/linux-arm64/384ff7382de624fb94dbaf6da11977bba1ecd427/out/vs/server/node/server.main.js:48:731)
    at listOnTimeout (node:internal/timers:581:17)
    at process.processTimers (node:internal/timers:519:7)
[33935 ms] [13:20:43] ptyHost was unable to resolve shell environment Error: Unable to resolve your shell environment in a reasonable time. Please review your shell configuration and restart.
    at Timeout.<anonymous> (file:///vscode/vscode-server/bin/linux-arm64/384ff7382de624fb94dbaf6da11977bba1ecd427/out/vs/server/node/server.main.js:48:731)
    at listOnTimeout (node:internal/timers:581:17)
    at process.processTimers (node:internal/timers:519:7)
[34056 ms] [13:20:43] ptyHost was unable to resolve shell environment Error: Unable to resolve your shell environment in a reasonable time. Please review your shell configuration and restart.
    at Timeout.<anonymous> (file:///vscode/vscode-server/bin/linux-arm64/384ff7382de624fb94dbaf6da11977bba1ecd427/out/vs/server/node/server.main.js:48:731)
    at listOnTimeout (node:internal/timers:581:17)
    at process.processTimers (node:internal/timers:519:7)
[37556 ms] [13:20:47] Installing extension 'github.vscode-pull-request-github'...
[37574 ms] [13:20:47] Getting Manifest... github.vscode-pull-request-github
[37708 ms] [13:20:47] Installing extension: github.vscode-pull-request-github {
  isMachineScoped: false,
  installPreReleaseVersion: false,
  isApplicationScoped: true,
  isBuiltin: false,
  installGivenVersion: false,
  installOnlyNewlyAddedFromExtensionPack: true,
  profileLocation: hn {
    scheme: 'file',
    authority: '',
    path: '/home/user/.vscode-server/extensions/extensions.json',
    query: '',
    fragment: '',
    _formatted: 'file:///home/user/.vscode-server/extensions/extensions.json',
    _fsPath: '/home/user/.vscode-server/extensions/extensions.json'
  },
  productVersion: { version: '1.94.2', date: '2024-10-09T16:08:44.566Z' }
}
[148550 ms] [13:22:38] Extension signature verification result for github.vscode-pull-request-github: Success. Executed: true. Duration: 109595ms.
[149805 ms] [13:22:39] Extracted extension to file:///home/user/.vscode-server/extensions/github.vscode-pull-request-github-0.98.0: github.vscode-pull-request-github
[149840 ms] [13:22:39] Renamed to /home/user/.vscode-server/extensions/github.vscode-pull-request-github-0.98.0
[150060 ms] [13:22:39] Extension installed successfully: github.vscode-pull-request-github file:///home/user/.vscode-server/extensions/extensions.json
[150091 ms] [13:22:39] Extension 'github.vscode-pull-request-github' v0.98.0 was successfully installed.
[150207 ms] [13:22:39] ptyHost was unable to resolve shell environment Error: Unable to resolve your shell environment in a reasonable time. Please review your shell configuration and restart.
    at Timeout.<anonymous> (file:///vscode/vscode-server/bin/linux-arm64/384ff7382de624fb94dbaf6da11977bba1ecd427/out/vs/server/node/server.main.js:48:731)
    at listOnTimeout (node:internal/timers:581:17)
    at process.processTimers (node:internal/timers:519:7)
```

</details>