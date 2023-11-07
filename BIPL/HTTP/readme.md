## Installeer Apache
```bash
sudo dnf install httpd -y
sudo firewall-cmd --runtime-to-permanent --add-service=http
sudo firewall-cmd --reload
```
## /etc/httpd/conf.d/www.bmc.test.conf
```conf
<VirtualHost *:80>
    ServerName www.bmc.test
    ServerAlias bmc.test

    DocumentRoot /var/www/bmc.test
    # Vervang "/pad/naar/je/html/bestanden" door het daadwerkelijke pad naar je HTML-bestanden

    <Directory "/var/www/bmc.test">
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```
## /var/www/bmc.test/index.html
```html
<html>
  <h1>Telnr. 0644543213</h1>
    <p>Bel alleen met spoed!</p>
</html>

```