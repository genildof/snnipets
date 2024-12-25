# 🛠️ ServerPip Snippets

A curated collection of personal system administration snippets and commands for Linux servers.

## 📦 Package Management

### Pip Package Management

#### Remove All User-Installed Pip Packages
```bash
pip3 freeze --user | cut -d "@" -f1 | xargs pip3 uninstall -y
```

#### Update All Outdated Pip Packages
```bash
pip3 --disable-pip-version-check list --outdated --format=json | \
python3 -c "import json, sys; print('\n'.join([x['name'] for x in json.load(sys.stdin)]))" | \
xargs -n1 pip install -U
```

## 💻 System Maintenance

### Kernel Management

#### Clean Old Kernel Versions
This script keeps the 4 most recent kernel versions and removes the rest:

```bash
#!/bin/bash

# Remove old kernel versions
sudo apt-get purge $(dpkg --list | grep -P -o "linux-image-\d\S+" | head -n-4)

# Clean up packages
sudo apt-get autoremove
sudo apt-get clean

# Update GRUB
sudo update-grub
```

## 📝 Usage Notes
- Always review commands before execution
- Backup important data before running system maintenance commands
- These snippets are tested on Debian-based systems

## 🤝 Contributing
Feel free to contribute by submitting pull requests or creating issues for improvements.

## ⚠️ Disclaimer
Use these snippets at your own risk. Always understand what a command does before running it on your system.
