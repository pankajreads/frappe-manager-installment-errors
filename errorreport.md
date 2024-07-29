# Error Report

## Summary of Issues

This report documents the errors encountered during the installation and setup of various software packages on the system.

## Error Details

### 1. **Unable to Locate Package code**

**Command:**
```
sudo apt install code
```

**Output:**
```
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
E: Unable to locate package code
```

**Solution:**
Ensure the repository is added correctly for code. code refers to Visual Studio Code, which can be added via the Microsoft repository:
```
sudo apt update
sudo apt install software-properties-common apt-transport-https wget
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
sudo apt update
sudo apt install code
```

### 2. **Error: Externally Managed Environment**

**Command:**
```
pip3 install frappe-manager
```

**Output:**
```
error: externally-managed-environment

× This environment is externally managed
╰─> To install Python packages system-wide, try apt install
    python3-xyz, where xyz is the package you are trying to
    install.
    
    If you wish to install a non-Debian-packaged Python package,
    create a virtual environment using python3 -m venv path/to/venv.
    Then use path/to/venv/bin/python and path/to/venv/bin/pip. Make
    sure you have python3-full installed.
    
    If you wish to install a non-Debian packaged Python application,
    it may be easiest to use pipx install xyz, which will manage a
    virtual environment for you. Make sure you have pipx installed.
    
    See /usr/share/doc/python3.11/README.venv for more information.

note: If you believe this is a mistake, please contact your Python installation or OS distribution provider. You can override this, at the risk of breaking your Python installation or OS, by passing --break-system-packages.
hint: See PEP 668 for the detailed specification.
```

**Solution:**
Use a virtual environment:
```
python3 -m venv vman
source vman/bin/activate
pip install frappe-manager
```

### 3. **Docker Daemon Not Running**

**Command:**
```
fm create project.pankaj
```

**Output:**
```
✅ fm directory doesn't exists! Created at -> /home/vboxuser/frappe
❌ Docker daemon not running. Please start docker service.
```

**Solution:**
Start the Docker service:
```
sudo systemctl start docker
sudo systemctl enable docker
```

### 4. **Docker Images Not Available Locally**

**Output:**
```
❌ Docker image 'ghcr.io/rtcamp/frappe-manager-frappe:v0.15.0' is not available locally
❌ Docker image 'ghcr.io/rtcamp/frappe-manager-nginx:v0.15.0' is not available locally
❌ Docker image 'redis:6.2-alpine' is not available locally
❌ Docker image 'ghcr.io/rtcamp/frappe-manager-mailhog:v0.8.3' is not available locally
❌ Docker image 'adminer:4' is not available locally
❌ Error Occured  projectofpankaj.localhost : Required docker images not available. Pull all required 
```

**Solution:**
Manually pull the required Docker images:
```
docker pull ghcr.io/rtcamp/frappe-manager-frappe:v0.15.0
docker pull ghcr.io/rtcamp/frappe-manager-nginx:v0.15.0
docker pull redis:6.2-alpine
docker pull ghcr.io/rtcamp/frappe-manager-mailhog:v0.8.3
docker pull adminer:4
```
