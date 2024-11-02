# Mod SEcurity


## Installation 

1. Installing the mod security package on a Debian based system:
```bash
sudo apt install libapache2-mod-security2 -y
```
2. After installing the mod security package, enable the mods security module
```bash
sudo a2enmod headers
```
3. Restart the Apache2 service
```bash
sudo systemctl restart apache2
```

## Configuration
1. Using a mod security configuration file
```bash
sudo cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf
```

## Setting up OWASP mod security Core Rule Set
The OWASP mod security Core Rule Set is available at https://github.com/SpiderLabs/owasp-modsecurity-crs
it can when enabled provide protection on against common vulnerabilities in web applications.

To Begin, run the following commands:

1. Delete the default rules that come with mod security by default
```bash
sudo rm -rf /usr/share/modsecurity-crs
```
2. Clone the OWASP-crs repository to `/usr/share/modsecurity-crs.` (make sure you have git installed)

```bash
sudo git clone https://github.com/coreruleset/coreruleset /usr/share/modsecurity-crs
```

3.  Rename the `crs-setup.conf.example` file to `ocrs-setup.conf`
```bash
sudo mv /usr/share/modsecurity-crs/crs-setup.conf.example /usr/share/modsecurity-crs/crs-setup.conf
```

4. Rename the `REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf.example` file to `REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf`
```bash
sudo mv /usr/share/modsecurity-crs/rules/REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf.example /usr/share/modsecurity-crs/rules/REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf
```
##  Mod Security in Apache2

To begin using Mod Security, run the following commands:

1. Edit the `/etc/apache2/mods-available/security2.conf` file to include `OWASP-CRS`.
```bash
sudo nano /etc/apache2/mods-available/security2.conf
```
2. Make sure you add where the `crs-setup.conf` file is located.  
```bash
<IfModule mod_security2_module>
    Include /usr/share/modsecurity-crs/crs-setup.conf
    Include /usr/share/modsecurity-crs/rules/*.conf
</IfModule>
```
3. Makes sure you add the previous command in the `/etc/apache2/sites-available/000-default.conf` file. 
```bash
SecRuleEngine On
<IfModule mod_security2_module>
    Include /usr/share/modsecurity-crs/crs-setup.conf
    Include /usr/share/modsecurity-crs/rules/*.conf
</IfModule>
```

and you will be all set with the OWASP mod security Core Rule Set.


## Conclusion
Congratulations, you have successfully installed and configured mod security for Apache2.


## References
https://www.youtube.com/watch?v=MB7nQrlP5Yc&t=6s
