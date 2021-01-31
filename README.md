# squidex-docker-setup
Quick setup of squidex on a docker VM

## ubuntu 18.04/20.04 

### Install docker

See: https://docs.docker.com/engine/install/ubuntu/

```
sudo apt-get -y update

sudo apt-get -y install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

sudo apt-get -y update
sudo apt-get -y install docker-ce docker-ce-cli containerd.io
```

### Run docker-compose

Download this repo to get started.

```
sudo apt-get -y install git

cd ~/
sudo git clone https://github.com/mattjcowan/squidex-docker-setup.git
```

Edit the `.env` file as needed. 

The following variables ARE required:

- SQUIDEX_DOMAIN=mycms.mydomain.com
- SQUIDEX_ADMINEMAIL=someadminuser@mydomain.com
- SQUIDEX_ADMINPASSWORD=lower_upper_special_char_and_number_password

Reference the [appsettings.json](https://github.com/Squidex/squidex/blob/master/backend/src/Squidex/appsettings.json) file to make any other
overrides as needed. Put these overrides in the `docker-compose.yml` file in the `environment` section of the `squidex_squidex` service section.

Each `json` indent can be overridden with a double underscore (e.g: __), for example:

```
{
    "abc": {
        "def": "hij"    
    }
}
```

Override with `ABC__DEF=hij`.

Once all environment variables are set, run docker-compose up:

```
cd ~/squidex-docker-setup
docker-compose up -d
```

## Inspect your docker containers as needed

Docker help with:

```
docker --help
# or
# docker {cmd} --help
docker ps --help
```

Enter a docker container with:

```
docker exec -it {first few letters of docker hash} bash
```

When in a docker container, you can install stuff if you're just experimenting:

```
apt-get update
apt-get install curl nano -y
```

