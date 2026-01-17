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
-   **Domain**: `www.deploymation.com`
    
-   **Site folder**: `/var/www/html/deploymation`
    
-   **Apache VirtualHost config** in `/etc/apache2/sites-available`
    
-   **Git-based deployment**
### Making things ready to host the Web site
#### Add a Host Record/A type record in the DNS Panel where you registered  your Domain. In my case I registered the Domain with name.com
<img src="/images/www-records.png" width="50%">

### Create a directory to host your website code
``` bash
sudo mkdir -p /var/www/html/deploymation
 ```
### Clone the Git repository into your current Linux directory
``` bash
git clone https://github.com/DriveIT-Tech/corp-website.git
```

### Copy the contents to Website directory
``` bash
sudo cp -r corp-website/* /var/www/html/deploymation
```
vs
``` bash
sudo cp -r corp-website/. /var/www/html/deploymation
```
#### Which one to use * or .
#### Asterisk copies:
-   All **non-hidden files and directories**
#### DOT copies:
- Hidden files & folders

It is better to use .

### Set correct ownership & permissions (CRITICAL)
```bash
sudo chown -R www-data:www-data /var/www/html/deploymation
sudo chmod -R 755 /var/www/html/deploymation
```

On Ubuntu:

-   **Apache** runs as `www-data`
    
-   Often **Nginx** also runs as `www-data`

