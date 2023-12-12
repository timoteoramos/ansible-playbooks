# Appliances Configuration

## pfSense as QEMU/KVM guest

As pfSense doesn't have some kind of API, I can't automate the entire process for now. You'll need to do some steps manually on the web panel. The playbook itself is simple to run, it'll install `qemu-guest-agent` package directly from FreeBSD package manager and it'll configure some initialization parameters.

```bash
# Install and configure the agent
ansible-playbook --limit pfsense -i ~/your-inventory.yml appliances/configuration/pfsense-qemu.yml
```

And then, you'll need to do some extra steps:

- Install `Shellcmd` from pfSense Package Manager
- Add a shellcmd on Service/Shellcmd: `service qemu-guest-agent start`
- On System / Advanced / Tunables, add the following tunable: `virtio_console_load` with value `YES`
- If you're using a VirtIO network adapter, you also need to change a setting in System / Advanced / Network: check the `Hardware Checksum Offloading` option

Finally, restart your pfSense VM.

## Toggle Proxmox enterprise repositories

With these playbooks, you can enable or disable Proxmox enterprise repositories. These repositories will be disabled unless you set the `enterprise_enabled` variable to `true`.

```bash
# Enable enterprise repository on PBS
ansible-playbook --limit proxmox -i ~/your-inventory.yml --extra-vars '{"enterprise_enabled":true}' appliances/configuration/proxmox-bs-toggle-er.yml

# Disable enterprise repository on PVE
ansible-playbook --limit proxmox -i ~/your-inventory.yml appliances/configuration/proxmox-ve-toggle-er.yml
```

## References

- [Install QEMU guest agent on pfSense - Bart's Blog](https://peperkamp.dev/articles/install_qemu_guest_agent_on_pfsense)
- [VirtIO Driver Support - pfSense Documentation](https://docs.netgate.com/pfsense/en/latest/virtualization/virtio.html)
