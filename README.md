# La Suite Numérique
How-To build La Suite Numérique: read [https://github.com/suitenumerique](https://github.com/suitenumerique)

# Pré-requis

## Install Python

```bash
# Update the list of products
sudo apt-get upgrade --yes
sudo apt-get update

sudo apt-get install -y powershell

ls -al /etc/os-release
cat /usr/lib/os-release | grep -i "PRETTY_NAME"

sudo apt-get install python3
python3 -m pip install -U pip
pip list

sudo apt-get install python3-venv
python3 -m venv --help
```

## OpenTofu

Read the [doc](https://opentofu.org/docs/intro/install/)

```bash
sudo snap install hello-world

# https://opentofu.org/docs/intro/install/standalone/
# https://get.opentofu.org/install-opentofu.sh -o install-opentofu.sh

OPEN_TOFU_VER=1.12
echo "Installing ToFu version " $OPEN_TOFU_VER

sudo snap install --classic opentofu
tofu version
```

## Git-Config setup

Cf [git-config.md](git-config.md)

## Clone Git repo

```bash
git clone git@github.com:$GH_USR/suitenumerique.git
```

#  À propos de LaSuite

Aujourd'hui, LaSuite est composée des produits principaux suivants:

- Messagerie - le client e-mail nouvelle génération des agents publics.
    - Cf [Messagerie.md](./Messagerie.md)

- Tchap - la messagerie instantanée et sécurisée de l'État, utilisée par plus de 600 000 agents. 
    - Cf [Tchap.md](Tchap.md)

- Visio - la solution de visioconférence, qui vous permet d'organiser des réunions en ligne en toute confiance et en toute sécurité.
    - Cf [Visio.md](Visio.md)

- Docs - l'éditeur de texte collaboratif qui privilégie le contenu sur la mise en forme.
    - Cf [Docs.md](Docs.md)

- Fichiers - l'outil qui vous permet de centraliser vos fichiers et de les partager avec les bonnes personnes.
    - Cf [Fichiers.md](Fichiers.md)

- Grist - le tableur collaboratif qui vous aide à structurer vos bases de données. Basé sur grist-core.
    - Cf [Grist.md](Grist.md)

- France Transfert - l'outil d'envoi et de réception de fichiers volumineux pensé pour les besoins de l'administration.
    - Cf [France-Transfert.md](France-Transfert.md)

Et d'autres outils annexes sont en cours de développement : Projets, Calendrier, Recherche, Transcription, la Régie, Messages, et l'Assistant IA.