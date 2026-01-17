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
```
### Web site details
-   **Domain**: `www.deploymation.com`
    
-   **Site folder**: `/var/www/html/deploymation`
    
-   **Apache VirtualHost config** in `/etc/apache2/sites-available`
    
-   **Git-based deployment**
### Making things ready to host the Web site
#### Add a Host Record/A type record in the DNS Panel where you registered  your Domain. In my case I registered the Domain with name.com
<img src="/images/www-records.png" width="50%">


