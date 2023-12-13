# Terminal Configuration

## Zshell

This playbook will try to install `zsh` and `nano` on your system and do some specific tweaks for a specified user. The user configuration will be omitted if you don't specify a user. I chose `nano` as the default editor because it's simple, popular and easy to use.

```bash
ansible-playbook --limit example -i ~/your-inventory.yml --extra-vars "setup_user=timoteoramos" config/terminal/zsh.yml
```
