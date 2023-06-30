FROM quay.io/kairos/kairos-ubuntu-20-lts:v2.2.2-k3sv1.25.10-k3s1

# Add all additional packages to install on kairos
RUN apt-get update && \
    apt-get install -y curl \
                       unzip \
                       iputils-ping \
                       tcpdump \
                       cron \
                       qemu-kvm \
                       libvirt-daemon-system \
                       libvirt-clients \
                       bridge-utils \
                       ca-certificates \
                       wget

RUN curl -sSLf https://raw.githubusercontent.com/openziti/ziti-tunnel-sdk-c/main/package-repos.gpg \
| gpg --dearmor \
| sudo tee /usr/share/keyrings/openziti.gpg >/dev/null && \
echo 'deb [signed-by=/usr/share/keyrings/openziti.gpg] https://packages.openziti.org/zitipax-openziti-deb-stable focal main' \
| sudo tee /etc/apt/sources.list.d/openziti.list >/dev/null && \
apt-get update && \
    apt-get install -y ziti-edge-tunnel
