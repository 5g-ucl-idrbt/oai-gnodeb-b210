# oai-gnodeb
# Build with `docker build`

## Resolve docker dependency using stagewise build
### Build Ran-base
1. 
```
sudo docker build . -f docker/Dockerfile.base.ubuntu18 -t ran-base:latest
sudo docker run -it --name=gnb ran-base
```
1. Inside container
```
/bin/sh oaienv
cd cmake_targets
./build_oai -I -w USRP --install-optional-packages
```
1. Track progress of installation in a separate terminal
```
sudo docker exec gnb tail -f /oai-ran/cmake_targets/log/uhd_install_log.txt
```
1. Exit from the current docker and check 
	1. `sudo docker ps --filter "name=<container name>"`
	1. `sudo docker commit <containerID> <ImageName>`
### Build Ran-build
```
sudo docker build . -f docker/Dockerfile.build.ubuntu18 -t ran-build:latest
# Build actual gnb-base
sudo docker build . -f docker/Dockerfile.gNB.ubuntu18 -t oai-gnb:latest
```
## Run with `docker compose`
```
sudo docker compose -f ci-scripts/yaml_files/sa_b200_gnb/docker-compose.yml

```
