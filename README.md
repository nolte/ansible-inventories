# ansible-inventories

## Managed Inventories

```yaml
---
- git: git@github.com:nolte/ansible-inventories.git
  version: v0.0.2.dev
  dst: ext_debs/ansible-inventories/
```

### Private Storage Box

Folder: ``./storagebox``

```bash
export HCLOUD_TOKEN=$(pass internet/hetzner.com/projects/personal_storage/token) && \
    export ANSIBLE_INVENTORY=$(pwd)/storagebox/prod/
```

### k3s Playground

```bash
export HCLOUD_TOKEN=$(pass internet/hetzner.com/projects/k3s/terraform-token) && \
    export ANSIBLE_INVENTORY=$(pwd)/k3s/dev
```

### Minecraft

Folder: ``./minecraft``

```bash
export HCLOUD_TOKEN=$(pass internet/hetzner.com/projects/minecraft/terraform-token) && \
    export ANSIBLE_INVENTORY=$(pwd)/minecraft/prod/
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

### Releasing

Must be executed from the ``develop`` branch.

```bash
pre-commit uninstall \
    && bump2version --tag release --commit \
    && git checkout master && git merge develop && git checkout develop \
    && bump2version --no-tag patch --commit \
    && git push origin master --tags \
    && git push origin develop \
    && pre-commit install
```
