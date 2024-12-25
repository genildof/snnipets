# Serverpip snnipets
Personal snnipets collection

### Remove all packages installed by pip
sysadmin@server1:~/dev$ pip3 freeze --user | cut -d "@" -f1 | xargs pip3 uninstall -y

### Remove all packages installed by pip
sysadmin@server1:~/dev$ pip3 --disable-pip-version-check list --outdated --format=json | python3 -c "import json, sys; print('\n'.join([x['name'] for x in json.load(sys.stdin)]))" | xargs -n1 pip install -U
