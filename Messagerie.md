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

#

