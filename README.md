# snnipets
Personal snnipets collection

### Remove all packages installed by pip
pip3 freeze --user | cut -d "@" -f1 | xargs pip3 uninstall -y
