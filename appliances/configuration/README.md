# Appliances Configuration

## pfSense as QEMU/KVM guest (pfsense-qemu.yml)

### Usage

As pfSense doesn't have some kind of API, I can't automate the entire process for now. You'll need to do some steps manually on the web panel. The playbook itself is simple to run, it'll install `qemu-guest-agent` package directly from FreeBSD package manager and it'll configure some initialization parameters.

```bash
ansible-playbook --limit pfsense -i ~/your-inventory.yml appliances/configuration/pfsense-qemu.yml
```

And then, you'll need to do some extra steps:

- Install `Shellcmd` from pfSense Package Manager
- Add a shellcmd on Service/Shellcmd: `service qemu-guest-agent start`
- On System / Advanced / Tunables, add the following tunable: `virtio_console_load` with value `YES`
- If you're using a VirtIO network adapter, you also need to change a setting in System / Advanced / Network: check the `Hardware Checksum Offloading` option

Finally, restart your pfSense VM.

### References

- [Install QEMU guest agent on pfSense - Bart's Blog](https://peperkamp.dev/articles/install_qemu_guest_agent_on_pfsense)
- [VirtIO Driver Support - pfSense Documentation](https://docs.netgate.com/pfsense/en/latest/virtualization/virtio.html)
