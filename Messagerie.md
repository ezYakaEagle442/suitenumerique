# Read Deployment repo docs

Cf [https://gitlab.mim-libre.fr/dimail/dimail-infra](https://gitlab.mim-libre.fr/dimail/dimail-infra/-/blob/main/ONBOARDING.md)


Voir le fork des repos :

[https://github.com/ezYakaEagle442/dimail-infra](https://github.com/ezYakaEagle442/dimail-infra)
[https://github.com/ezYakaEagle442/dimail-infra-template](https://github.com/ezYakaEagle442/dimail-infra-template)

# Git fork dimail-infra

on Github, create a repo "dimail-client.git"

```sh
pwd
git clone --mirror https://gitlab.mim-libre.fr/dimail/dimail-client.git

cd dimail-client.git
git push --mirror git@github.com:$GH_USR/dimail-client.git

cd ..
rm -rf dimail-client.git

git clone git@github.com:$GH_USR/dimail-client.git
cd dimail-client
```

# Setup the development environment

## Create a python environment

```sh
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Switch to the python venv

```sh
source .venv/bin/activate
# Install Clientèle: https://docs.clientele.dev/install/#pip_1
pip install clientele
pip install "clientele[cli]"
clientele --help
clientele version
```


## Leave the python env (switch back to the default python interpreter)

```sh
deactivate
```

## Update the "raw" client as managed by clientele
```sh
cd ~
pwd

apt list -v '*clientele*'
pip install --break-system-packages clientele
pip install --break-system-packages "clientele[cli]"

sudo apt install pipx --yes

# Install clientele from outside the project directory to avoid import conflicts
cd ~
pwd
ls -al
pipx install clientele --force
pipx install "clientele[cli]" --force
clientele --help
clientele version

cd dimail/raw

clientele start-api -u https://api.osprod.dimail1.numerique.gouv.fr/openapi.json -a -r -o .
# clientele start-api -u http://localhost:8000/openapi.json -a -r -o .
sed -i -e 's/ = list\[\(.*\)\]/ = pydantic.RootModel[list[\1]]/g' schemas.py

openapi-python-client generate --url http://localhost:8000/openapi.json --output-path dimail/raw2 --overwrite

```

# Git fork CONFIG_REPOSITORY_URL

Read the [doc](https://github.com/ezYakaEagle442/dimail-infra-template/tree/renovate/configure)

```sh
pwd
git clone --mirror https://gitlab.mim-libre.fr/dimail/dimail-infra-template.git

cd dimail-infra-template.git
git push --mirror git@github.com:$GH_USR/dimail-infra-template.git

cd ..
rm -rf dimail-infra-template.git

git clone git@github.com:$GH_USR/dimail-infra-template.git
cd dimail-infra-template

git checkout main
```

# Git fork Dimail-infra

Read the [doc](https://gitlab.mim-libre.fr/dimail/dimail-infra/-/blob/main/README.md)

```sh
pwd
git clone --mirror https://gitlab.mim-libre.fr/dimail/dimail-infra.git

cd dimail-infra.git
git push --mirror git@github.com:$GH_USR/dimail-infra.git

cd ..
rm -rf dimail-infra.git

git clone git@github.com:$GH_USR/dimail-infra/
cd dimail-infra/

git checkout main
```


# Install and configuration of your computer and environment

Read the [doc](https://github.com/ezYakaEagle442/dimail-infra/blob/main/ONBOARDING.md)

##

```sh
pwd
cd ~
python3 -m venv .venv source .venv/bin/activate 
cd ../dimail-infra-template/ 


cd 40_ansible/ 
python3 -m pip install -r requirements.txt ansible-galaxy install -r requirements.yml

```

# Deploy on Outscale

## Install Outscale CLI

Read the [doc](https://docs.outscale.com/fr/userguide/Installer-et-configurer-OSC-CLI.html)
and [CLI Ref](https://github.com/outscale/osc-cli/blob/main/README.md)

```sh

apt list -v '*osc-sdk'

python3 -m venv .venv
source .venv/bin/activate

pip3 install osc-sdk

cd ~
mkdir ".osc"

export ACCESSKEY="<CONFIDENTIAL ACCESS KEY>"
export SECRETKEY="<CONFIDENTIAL SECRET KEY>"

cat <<EOF >> config.json
{
    "default": {
        "access_key": "$ACCESSKEY",
        "secret_key": "$SECRETKEY",
        "host": "outscale.com",
        "https": true,
        "method": "POST",
        "region": "eu-west-2"
    }
}
EOF

# envsubst < config.json > deploy/config.json

cat config.json
osc-cli --version

```


## Run OpenTofu

30_outscale - Outscale tofu stack

```sh

# The configuration path for the environment.
export DIMAIL_CONFIG_PATH="../dimail-infra-template"

# The environment (e.g., ovhprod, ovhdev, osdev, osdev2, osprod).
export DIMAIL_ENV="outscaledev"

# - The type of environment (e.g., prod).
export DIMAIL_ENVTYPE="dev"

# The hosting type.
export DIMAIL_HOSTING="outscale"

mkdir $DIMAIL_CONFIG_PATH/env-$DIMAIL_ENV

export OS_USERNAME="openstack-username"
export OS_PASSWORD="openstack-password"
export OS_PROJECT_NAME="openstack-projectname"
export OS_PROJECT_ID="openstack-projectid"

export OS_PROJECT_DOMAIN_NAME="Default"
export OS_USER_DOMAIN_NAME="Default"
export OS_AUTH_URL="https://auth.outscale.com"
export OS_PROJECT_DOMAIN_ID="default"
export OS_REGION_NAME="eu-west-2a"
export OS_INTERFACE="public"
export OS_IDENTITY_API_VERSION="3"

make help

# Init: 
make init

# Plan: 
make plan

# Apply: *
make apply

# Autres Commandes: make check checks environment, every operation launch it for you.
#Tests: 
make test runs some tests on the ansible stack
```

```sh

```