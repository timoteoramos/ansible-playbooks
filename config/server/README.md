# Server Configuration

## Docker

This playbook will try to install `docker` on your system with IPv6 support. You can change the IPv6 bridge network specifying the optional `docker_ipv6_bridge` variable.

```bash
ansible-playbook --limit docker -i ~/your-inventory.yml --extra-vars "docker_ipv6_bridge=2001:db8:1::/64" config/server/docker.yml
```
