# SSH Remote Server Setup

## 📌 Overview

This project demonstrates how to set up a remote Linux server and configure SSH access using multiple SSH keys.

---

## 🖥️ Server Setup

* Created an Ubuntu 22.04 EC2 instance on AWS
* Enabled SSH access (port 22)

---

## 🔑 SSH Key Creation

Generated two SSH key pairs on local machine:

```bash
ssh-keygen -t rsa -b 4096 -f ~/.ssh/devops-key-1
ssh-keygen -t rsa -b 4096 -f ~/.ssh/devops-key-2
```

---

## 👤 User Configuration

* Created a new user `devops`
* Granted sudo access

```bash
sudo adduser devops
sudo usermod -aG sudo devops
```

---

## 🔐 SSH Configuration

Added both public keys to server:

```bash
nano ~/.ssh/authorized_keys
```

Content:

```
<devops-key-1.pub>
<devops-key-2.pub>
```

Set permissions:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

---

## 🔌 Connection Test

Connected using both keys:

```bash
ssh -i ~/.ssh/devops-key-1 devops@<server-ip>
ssh -i ~/.ssh/devops-key-2 devops@<server-ip>
```

---

## ⚙️ SSH Config Setup

Configured `~/.ssh/config`:

```bash
Host myserver-key1
    HostName <server-ip>
    User devops
    IdentityFile ~/.ssh/devops-key-1

Host myserver-key2
    HostName <server-ip>
    User devops
    IdentityFile ~/.ssh/devops-key-2
```

Connected using:

```bash
ssh myserver-key1
ssh myserver-key2
```

---

## 🛡️ Security (Stretch Goal)

Installed Fail2Ban to prevent brute-force attacks:

```bash
sudo apt update
sudo apt install fail2ban -y
sudo systemctl enable fail2ban
```

---

## ✅ Final Outcome

* Successfully connected to the server using two SSH keys
* Configured SSH alias for easy access
* Secured server with Fail2Ban

---

## ⚠️ Important Note

Private keys are not included in this repository for security reasons.

https://roadmap.sh/projects/ssh-remote-server-setup
