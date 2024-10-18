# syntax=docker/dockerfile:1.4
FROM --platform=arm64 rubensa/ubuntu-tini-dev

# VSCode hack
RUN <<EOT
#!/usr/bin/env bash
if [ -n \"\$VSCODE_RESOLVING_ENVIRONMENT\" ]; then
  return
fi

$(cat /home/${USER_NAME}/.bashrc)" > /home/${USER_NAME}/.bashrc
EOT