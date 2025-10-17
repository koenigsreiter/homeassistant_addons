# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH K3S_VERSION
RUN apk add --no-cache curl bash jq iptables && \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}" && \
    curl -sSLf https://github.com/k3s-io/k3s/releases/download/${K3S_VERSION}/k3s -o /usr/local/bin/k3s

# Copy root filesystem
COPY rootfs /

RUN chmod +x /etc/services.d/k3s/run /etc/services.d/k3s/finish