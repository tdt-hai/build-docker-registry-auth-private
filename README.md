# build-docker-registry-auth-private

## Setup on linux
1. Clone the repo.
2. Init cert registry and auth
```shell
mkdir /zfsdata/certs
cd /zfsdata/certs
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout registry.key -out registry.pem
```
3. Run docker compose file.

```shell
docker-compose -f docker-registry.yml up -d
```
```shell
docker-compose -f docker-auth.yml up -d
```
## Config examble on docker-auth
Configuration file is `config/auth_config.yml`.
See the example config files in [cesanta/docker_auth](https://github.com/cesanta/docker_auth/tree/main/examples)
## Enable insecure-registry in client
1. Linux (Unverified)
```shell
sudo cat > /etc/docker/daemon.json << EOF
{
  "insecure-registries" : ["<ip>:5000"]
}
EOF
```
```shell
sudo service docker restart
```
2. Windows (Unverified)
```shell
C:\ProgramData\docker\config\daemon.json

ADD 

{
  "insecure-registries" : ["<ip>:5000"]
}
```
## Preferences

docker-registry at https://docs.docker.com/registry/deploying/.

docker-auth at https://github.com/cesanta/docker_auth.