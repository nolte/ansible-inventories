# ansible-inventories

Used at different locations, like some ArgoWorkflow`s, AWX Jobs or Local development

## Managed Inventories

The diffrent Inventories are located inside the `./src` subdirectory. More Informations about Ansible Inventiries at [docs.ansible.com](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#how-to-build-your-inventory)

### Local

Folder: ``./local``

```bash
export ANSIBLE_INVENTORY=$(pwd)/src/local/
```

### Minecraft

Folder: ``./minecraft``

```bash
export HCLOUD_TOKEN=$(pass internet/hetzner.com/projects/minecraft/terraform-token) && \
    export ANSIBLE_INVENTORY=$(pwd)/src/minecraft/prod/
```

## Development

```bash
virtualenv -p python3 ~/venvs/ansible-vagrant
source ~/venvs/ansible-vagrant/bin/activate
pip install -r requirements.txt
pre-commit install
```

### Testing Connection 

```bash
ansible all -m ping
```

Testing a dedicated element, from the inventory.

```bash
ansible rpi2hifybarry -e ansible_user=pi -e ansible_ssh_user=pi -m ping
```
