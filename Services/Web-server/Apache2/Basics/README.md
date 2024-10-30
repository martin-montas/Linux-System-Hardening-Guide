# Apache2 Security
This repository contains security and best practices for Apache2 and other Apache2 
related tools.

#### Prequisites
- Apache2 should be installed on your system.
- you should have a basic understanding of Apache2 and its commands.

### 1.0 Disable Unwanted Services
All web servers should only be used as a web server. Disabling unwanted services reduces 
vulnerabilities and attack surface on the system.

1. Listing all enabled and running services
```bash
systemctl list-units --type=service
```
2. Disabling a service
```bash
systemctl disable <service_name>
```

### 2.0 Ensure the Log Config Module Is Enabled
The Log Config Module is important since it enables logging every request to the web server which 
help us keeping everything in check.
1. Check if the Log Config Module is enabled
```bash
apache2ctl -M | egrep 'log_config'
```
2. Enable the Log config module
```bash
a2enmod log_config
```

### 3.0 Hide Version and OS Details from HTTP Headers
Hiding the version and OS details from HTTP headers keeps unwanted eyes from enumarating the system
and the web server. 
1. Edit/add the following lines in the config file:
```bash
ServerSignature Off
ServerTokens Prod
```
2. Open the config file:
```bash
sudo systemctl restart apache2  # For Ubuntu/Debian
sudo systemctl restart httpd    # For CentOS/Red Hat
```

### Conclusion
These are just some of the basics for Apache2 security. There are still a plethora of security configurations
for Apache2 and other tools as well.
