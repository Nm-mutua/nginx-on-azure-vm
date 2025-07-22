# Azure Linux Web Server Project Deployment

This project demonstrates how to deploy an Apache web server on a Linux virtual machine hosted in Microsoft Azure. The deployment is done using the Azure CLI and includes SSH access, network configuration, and basic web server setup.

---

##  Technologies Used

- Microsoft Azure
- Azure CLI
- Linux (Ubuntu 20.04 LTS)
- Apache
- Bash
- SSH
- UFW & Fail2Ban (to prevent brute force attacks)
- Git & GitHub

---

##  Steps to Deploy

### 1. Create a Resource Group
```bash
az group create --name myResourceGroup --location "Central US"
```

### 2. Create a Linux Virtual Machine
```bash
az vm create \
  --resource-group myResourceGroup \
  --name myLinuxVM \
  --image Ubuntu2204 \
  --size Standard_B1s
  --admin-username azureuser \
  --generate-ssh-keys
  ```

### 3. Open Port 80 for HTTP
```bash
az vm open-port --resource-group myResourceGroup --name myLinuxvm --port 80
```

### 4. SSH into the VM
```bash
ssh azureuser@52.230.189.5
```

### 5. Install Web Server (Apache)
```bash
sudo apt update
sudo apt install apache2 -y
sudo systemctl enable apache2
sudo systemctl start apache2
```

### 6. Test in Browser
      Visit
http://52.230.189

# Security Hardening
### 1. Created a Non-root Admin User
```bash
sudo adduser adminuser
sudo usermod -aG sudo adminuser
```
### 2. Disabled Root Login Over SSH
```bash
sudo nano /etc/ssh/sshd_config
# Changed: PermitRootLogin no
sudo systemctl restart ssh
```

### 3. Enabled UFW Firewall
```bash
sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw enable
sudo ufw status
```
### 4. Installed and Enabled Fail2Ban
```bash
sudo apt install fail2ban -y
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```
## Screenshots

















