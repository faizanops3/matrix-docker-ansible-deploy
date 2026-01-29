# Full Guide

## 1. Update and install packages

```sh
apt update
apt install -y git python3 python3-pip sudo

# Install Ansible and Passlib
apt install -y ansible-core python3-passlib
```

- `ansible --version`

## 2. Firewall Rules

```csv
Description,Protocol,Port / Range,Sources,Why?
SSH,TCP,22,0.0.0.0/0 (Any),CRITICAL: Remote Access
HTTP,TCP,80,0.0.0.0/0,Let's Encrypt / Web Redirection
HTTPS,TCP,443,0.0.0.0/0,Main Web Interface
HTTP/3,UDP,443,0.0.0.0/0,HTTP/3 QUIC Support
Federation,TCP,8448,0.0.0.0/0,Server-to-Server communication
Federation,UDP,8448,0.0.0.0/0,Required by documentation
TURN (Call),TCP,3478,0.0.0.0/0,Audio/Video Signaling
TURN (Call),UDP,3478,0.0.0.0/0,Audio/Video Signaling
TURN (Secure),TCP,5349,0.0.0.0/0,Secure Audio/Video Signaling
TURN (Secure),UDP,5349,0.0.0.0/0,Secure Audio/Video Signaling
TURN Relay,UDP,49152-49172,0.0.0.0/0,The actual audio/video data stream
```

## 3. Clone the repository

```sh
git clone https://github.com/faizanops3/matrix-docker-ansible-deploy.git

cd matrix-docker-ansible-deploy
```

## 4. Configure the playbook

- which i have done "premade".

```
inventory\host_vars\matrix.bloomi5.com\vars.yml
inventory\hosts
```

## 5. Run the playbook

### Update Ansible Roles

```sh
rm -rf roles/galaxy; ansible-galaxy install -r requirements.yml -p roles/galaxy/ --force
```

### Run installation command

Then, run the command below to start installation:

```sh
export ANSIBLE_HOST_KEY_CHECKING=False
```

```sh
ansible-playbook -i inventory/hosts setup.yml --tags=install-all,ensure-matrix-users-created,start --ask-pass
```
