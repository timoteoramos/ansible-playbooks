# Ansible Playbooks

These are my personal Ansible playbooks that I use more frequently. Feel free to use, copy or learn something with these playbooks.

## Startup reference

First of all, you need to configure your `/etc/ansible/hosts`:

```toml
[example_host_group]
your_host ansible_host=yourhost.example.local ansible_user=root
```

It's expected to run these playbooks on root user, specially the ones that aren't related to Docker.

Here are some usage examples:

```bash
# Configure the most common settings on Linux (it's expected to work on systems based on Debian, RHEL and Alpine)
ansible-playbook --limit your_host --extra-vars "timezone=America/Araguaina" linux/configure-system.yml

# Configure an user with useful tweaks (tmux, zsh and more)
ansible-playbook --limit your_host --extra-vars "ssh=your_user" linux/update-user-profile.yml

# Initialize a Swarm cluster
ansible-playbook --limit your_host --extra-vars "advertise_addr=enp1s0 data_path_addr=enp1s0" swarm/cluster-init.yml
```

## Development reference

```bash
# Validate playbooks
find . -type f -name \*.yml -exec ansible-lint {} \;
```
