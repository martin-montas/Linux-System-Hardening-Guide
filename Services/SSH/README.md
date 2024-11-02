# Debian-Based System

### 1.0 Setting No Root Login Over SSH
Edit `/etc/ssh/sshd_config` and set `PermitRootLogin no`.
By doing this, you are preventing una
minimizing the risk of malicious attacks.

### 2.0 Allowing Secure Shell From our System  
We will be using `ufw` firewall to allow access to our system. The following command den
connections, allowing all outgoing connections, and allowing ssh login from our local IP
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow from <YOUR_LOCAL_IP> to any port 22
sudo ufw enable
```

### 3.0 Use Fail2Ban to Prevent SSH Brute-Force Attacks
Here is how to set up Fail2Ban in Debian-based systems.
1. Install Fail2Ban
```bash
sudo apt install fail2ban
```
2. Create a configuration file for Fail2Ban
```bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```
3. Enable SSH protection in /etc/fail2ban/jail.local by ensuring the following is set:
```bash
[sshd]
enabled = true
```
4. Restart and enable Fail2Ban service
```bash
sudo systemctl start  fail2ban
sudo systemctl enable fail2ban
```

### 4.0 Use Logging and Monitoring
Regularly monitor and log SSH activity on the system and be in the alert zone for unusual activities.

1. How to Enable SSH Logging: In /etc/ssh/sshd_config, set:
```bash
LogLevel VERBOSE
```
2. Logs can be viewed using:
```bash
cat /var/log/auth.log
```
