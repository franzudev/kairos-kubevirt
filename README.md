# Kairos
This repo is used to install and configure Kairos OS on edge nodes.

## Image Customization
In order to customize Kairos OS with additional packages, a base kairos image needs to be customized using `Dockerfile` and the customized imaged needs to be pushed on a registry. Currently the registry must be public because during installation no authentication is provided against the registry.

### Requirements
- docker

### Procedure
Run the following commands
```shell
cd stage

docker build -t <DOCKER_REPO>/kairos-custom-image .

docker push <DOCKER_REPO>/kairos-custom-image

# Edit the file stage/config.yaml and replace the occurences of <docker-repo>, <docker-image> and <ziti-token> with the necessary values
vim config.yaml

docker run -v $PWD/config.yaml:/config.yaml \
  -v $PWD/build:/tmp/auroraboot \
  -v /var/run/docker.sock:/var/run/docker.sock \
  --rm -ti quay.io/kairos/auroraboot \
  --set "artifact_version=v2.2.1" \
  --set "release_version=v2.2.1" \
  --set "disable_http_server=true" \
  --set "repository=kairos-io/kairos" \
  --set "disable_netboot=true" \
  --cloud-config /config.yaml \
  --set "state_dir=/tmp/auroraboot" \
  --set "flavor=ubuntu-20-lts"
```

When the process is finished you can find the iso to flash on USB in `stage/build/iso/kairos.iso.custom.iso`

