# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH
RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"


# Install dependencies and K3s
RUN apk add --no-cache curl bash jq iptables \
 && curl -sfL https://get.k3s.io -o /install-k3s.sh \
 && chmod +x /install-k3s.sh

# Copy root filesystem
COPY rootfs /

COPY run_install.sh /run_install.sh
RUN chmod +x /run_install.sh /etc/services.d/k3s/run /etc/services.d/k3s/finish