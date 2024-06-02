# Pop!_OS Dev Playbook

This playbook is based upon https://github.com/crbanman/popos-dev-playbook that is used to setup my Pop!_OS dev environment.

## Prerequisites

You will need `pip` and `ansible` installed on your machine which can be done with the following commands:

```console
sudo apt install python3-pip
pip install --user ansible
export PATH=$PATH:~/.local/bin
```

## Installation

Download or clone this repository to your local drive.

```console
git clone https://github.com/joshm998/popos-dev-playbook.git
cd popos-dev-playbook
```

Install dependencies:

```console
ansible-galaxy install -r requirements.yml
```

## Usage

1. Make a copy of `default.config.yml` with the name `config.yml` and change the configurations you want to use.

1. Run the playbook with the command and enter your user account password when prompted:

   ```console
   ansible-playbook main.yml --ask-become-pass
   ```

1. Restart your machine.

## Manual changes

There are some things that I haven't been able to automate yet.

### Set node version

Download and set currently used `node` version with `nvm`. This should theoretically be handled by the playbook, but it doesn't.

```console
nvm install --lts
nvm use --lts
```

### Register SSH Keys

Add ssh keys. For better or worse I backup my keys, so I need to copy them to `~/.ssh/` and add them to the `ssh-agent`.

1. Set the the appropriate file permissions for each key:

   ```command
   chmod 400 ~/.ssh/id_ed25519
   ```

1. Start the ssh agent

    ```command
    eval "$(ssh-agent -s)"
    ```

1. For each key run `ssh-add`

   ```command
   ssh-add ~/.ssh/id_ed25519
   ```

### Run JetBrains Toolbox

Toolbox needs to be run once from the command line so the system can register the AppImage.

```command
/opt/jetbrains-toolbox
```