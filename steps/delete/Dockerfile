FROM alpine:3
RUN set -eux ; \
    mkdir -p /tmp/ni && \
    cd /tmp/ni && \
    wget https://packages.nebula.puppet.net/sdk/ni/v1/ni-v1-linux-amd64.tar.xz && \
    wget https://packages.nebula.puppet.net/sdk/ni/v1/ni-v1-linux-amd64.tar.xz.sha256 && \
    echo "$( cat ni-v1-linux-amd64.tar.xz.sha256 )  ni-v1-linux-amd64.tar.xz" | sha256sum -c - && \
    tar -xvJf ni-v1-linux-amd64.tar.xz && \
    mv ni-v1*-linux-amd64 /usr/local/bin/ni && \
    cd - && \
    rm -fr /tmp/ni
RUN apk --no-cache add bash ca-certificates curl git jq openssh && update-ca-certificates
RUN ["/bin/bash", "-c", "set -eux\nmkdir -p /tmp/helm \u0026\u0026 \\\n  cd /tmp/helm \u0026\u0026 \\\n  curl -L -o helm.tar.gz https://get.helm.sh/helm-v2.17.0-linux-amd64.tar.gz \u0026\u0026 \\\n  echo \"$( curl -sL https://get.helm.sh/helm-v2.17.0-linux-amd64.tar.gz.sha256 )  helm.tar.gz\" | sha256sum -c - \u0026\u0026 \\\n  tar -xvzf helm.tar.gz \u0026\u0026 \\\n  mv linux-amd64/helm /usr/local/bin/helm \u0026\u0026 \\\n  cd - \u0026\u0026 \\\n  rm -fr /tmp/helm\n"]
COPY "./step.sh" "/nebula/helm-step-delete.sh"
ENTRYPOINT []
CMD ["/bin/bash", "/nebula/helm-step-delete.sh"]

LABEL "org.opencontainers.image.title"="Delete Helm release"
LABEL "org.opencontainers.image.description"="The Helm delete step deletes a Helm release in a Kubernetes cluster."
LABEL "com.puppet.nebula.sdk.version"="v1"
