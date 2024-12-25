# 🛠️ ServerPip Snippets

A curated collection of personal system administration snippets and commands for Linux servers.

## 🐍 Python Environment Management

### Virtual Environment Setup
```bash
# Create a new virtual environment
python3 -m venv .venv

# Activate the virtual environment
source .venv/bin/activate   # Linux/Mac
.venv\Scripts\activate      # Windows

# Deactivate when finished
deactivate
```

### Package Installation
```bash
# Install individual packages
pip install package_name

# Install from requirements.txt
pip install -r requirements.txt

# Generate requirements.txt
pip freeze > requirements.txt
```

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

## 🌿 Git Version Control

### Initial Setup
```bash
# Initialize new repository
git init

# Configure global user
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Add SSH key to GitHub
cat ~/.ssh/id_rsa.pub    # Copy this to GitHub SSH keys section
```

### Basic Git Operations
```bash
# Add files
git add filename         # Add specific file
git add .               # Add all files

# Remove files
git rm filename         # Remove from git and filesystem
git rm --cached filename # Remove from git only

# Commit changes
git commit -m "Your commit message"

# Push to remote
git push origin main
```

## 🐳 Docker Commands

### Basic Docker Operations

| Command | Description |
|---------|-------------|
| `docker build -t image-name .` | Creates a new Docker image from a Dockerfile in the current directory |
| `docker-compose up` | Starts all services defined in docker-compose.yml with console output |
| `docker-compose up -d` | Starts all services in detached mode (background) |
| `docker-compose down` | Stops and removes all containers, networks created by up |
| `docker ps` | Lists all running containers |
| `docker logs container-name` | Shows logs for a specific container |

### Docker Cleanup Commands

| Command | Description |
|---------|-------------|
| `docker system prune --all` | Removes all unused containers, networks, images, and build cache |
| `docker container prune` | Removes all stopped containers |
| `docker image prune` | Removes all dangling images (unused and untagged) |

## 🔧 System Administration

### Service Management
```bash
# Check service status
systemctl status nginx
systemctl status gunicorn

# Start/Stop/Restart services
systemctl start service_name
systemctl stop service_name
systemctl restart service_name
```

### Network Troubleshooting
```bash
# Check active TCP ports
lsof -i tcp
netstat -tulpn

# Test HTTP response
curl -I http://localhost
curl -I https://yourdomain.com

# Check server info
hostname -I          # Get IP addresses
hostname             # Get hostname
ip addr show        # Detailed network interfaces
```

### Process Management
```bash
# View and manage processes
htop                # Interactive process viewer
ps aux | grep process_name
kill process_id
killall process_name
```

### User Management
```bash
# Create new user
useradd -m username    # -m creates home directory

# Add user to sudo group
usermod -aG sudo username

# Change password
passwd username

# Switch user
su - username
```

### File Permissions
```bash
# Make script executable
chmod +x script.sh

# Change file ownership
chown user:group filename
chown -R user:group directory    # Recursive

# Common permission patterns
chmod 755 script.sh    # rwxr-xr-x
chmod 644 file.txt     # rw-r--r--
chmod 600 id_rsa       # rw-------
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
- When creating shell scripts, remember to make them executable with `chmod +x`
- Always verify services status after configuration changes
- Regularly monitor system logs for issues

## 🤝 Contributing
Feel free to contribute by submitting pull requests or creating issues for improvements.

## ⚠️ Disclaimer
Use these snippets at your own risk. Always understand what a command does before running it on your system.
