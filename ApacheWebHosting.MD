# Install Apache2
``` bash
sudo apt update
sudo apt upgrade -y
sudo apt install apache2

### Verify Apache2 running status, press q to quit
sudo systemctl status apache2

### Install Certbot, which automatically configures an SSL Cert from Let's Encrypt
sudo apt install certbot python3-certbot-apache -y

### Verify the version
certbot --version

### Install latest Git
git --version
### sudo add-apt-repository ppa:git-core/ppa
sudo add-apt-repository ppa:git-core/ppa -y
sudo apt update
sudo apt install git -y
git --version
```
###
### Web site details
-   **Domain**: `www.devopsrelay.com`
    
-   **Site folder**: `/var/www/html/devopsrelay`
    
-   **Apache VirtualHost config** in `/etc/apache2/sites-available`
    
-   **Git-based deployment**
### Making things ready to host the Web site
#### Add a Host Record/A type record in the DNS Panel where you registered  your Domain. In my case I registered the Domain with name.com
<img src="/images/www-records.png" width="50%">

### Create a directory to host your website code
``` bash
sudo mkdir -p /var/www/html/devopsrelay
 ```
### Clone the Git repository into your current Linux directory
``` bash
git clone https://github.com/DriveIT-Tech/corp-website.git
```

### Copy the contents to Website directory
``` bash
sudo cp -r corp-website/* /var/www/html/devopsrelay
```
vs
``` bash
sudo cp -r corp-website/. /var/www/html/devopsrelay
```
#### Which one to use * or .
#### Asterisk copies:
-   All **non-hidden files and directories**
#### DOT copies:
- Hidden files & folders

It is better to use .

### Set correct ownership & permissions (CRITICAL)
```bash
sudo chown -R www-data:www-data /var/www/html/devopsrelay
sudo chmod -R 755 /var/www/html/devopsrelay
```

On Ubuntu:

-   **Apache** runs as `www-data`
    
-   Often **Nginx** also runs as `www-data`

## Tell Apache about how to host this website
### Create Apache VirtualHost configuration
```bash
sudo nano /etc/apache2/sites-available/devopsrelay.conf
```
Paste the following (adjust if needed):
```bash
<VirtualHost *:80>
    ServerName devopsrelay.com
    ServerAlias www.devopsrelay.com

    DocumentRoot /var/www/html/devopsrelay

    <Directory /var/www/html/devopsrelay>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/devopsrelay_error.log
    CustomLog ${APACHE_LOG_DIR}/devopsrelay_access.log combined
</VirtualHost>
```
Save and exit. Control+o, Control+x in nano editor
### Enable the site & required modules
```bash
sudo a2enmod rewrite
sudo a2ensite devopsrelay.conf
```

### Disable Default site that comes installed with Apache
```bash
sudo a2dissite 000-default.conf
```

### reload Apache for the changes to take effect
```bash
sudo systemctl reload apache2
```
### Validate Apache configuration
```bash
sudo apachectl configtest
```
### Test the website
http://www.deployment.com

http://deployment.com

### Enable HTTPS
```bash
sudo certbot --apache
```
Follow the onscreen instructions and complete HTTPS deployment

## Enable port 80/443 or HTTP/HTTPS Traffic to your EC2 Instance
<img src="/images/aws-http-https-rules.png" width="50%">
