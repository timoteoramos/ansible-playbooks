# Appliances Setup

## FreeIPA

This playbook will install and configure a FreeIPA server on a Red Hat based distro. It was tested on Rocky Linux 9, but it's expected to work in Alma Linux too, and also RHEL.

```bash
# Install a server a DNS server with a forwarder (you can specify more than one, if you need)
ansible-playbook --limit ipaserver -i ~/your-inventory.yml --extra-vars "server_domain=example.domain ipa_admin_password=yourpassword ipa_ds_password=yourpassword ipa_dns_forwarders=192.168.0.1" appliances/setup/freeipa.yml

# Install a server a DNS server without a forwarder (you just need to omit the variable)
ansible-playbook --limit ipaserver -i ~/your-inventory.yml --extra-vars "server_domain=example.domain ipa_admin_password=yourpassword ipa_ds_password=yourpassword" appliances/setup/freeipa.yml

# Install a server without a DNS server
ansible-playbook --limit ipaserver -i ~/your-inventory.yml --extra-vars "server_domain=example.domain ipa_admin_password=yourpassword ipa_ds_password=yourpassword ipa_dns_enabled=false" appliances/setup/freeipa.yml
```

## Proxmox

These 2 playbooks will install and configure Proxmox systems: the Backup Server (`proxmox-bs.yml`) and Virtual Environment (`proxmox-ve.yml`). Both are purely based on their respective official documentations.

```bash
# Install a Proxmox Backup Server
ansible-playbook --limit pbs-01 -i ~/your-inventory.yml --extra-vars "server_domain=example.domain" appliances/setup/proxmox-bs.yml

# Install a Proxmox Virtual Environment
ansible-playbook --limit pve-01 -i ~/your-inventory.yml --extra-vars "server_domain=example.domain kernel_version=6.2" appliances/setup/proxmox-ve.yml
```

## References

- [ipa-server-install(1) - Linux man page](https://linux.die.net/man/1/ipa-server-install)
- [Installation - Proxmox Backup Documentation](https://pbs.proxmox.com/docs/installation.html)
- [Install Proxmox VE on Debian 12 Bookworm - Proxmox VE](https://pve.proxmox.com/wiki/Install_Proxmox_VE_on_Debian_12_Bookworm)

## Further Reading

- [Active_Directory_trust_setup - FreeIPA documentation](https://www.freeipa.org/page/Active_Directory_trust_setup)
