# utilitystack
A bunch of scripts, snippets and codes that makes my devOps esier.

<h1>Create a new wordpress site with client name and virtual host configuration in apache</h1>

#!/bin/bash

# Descargar la última versión de WordPress
wget https://wordpress.org/latest.tar.gz

# Guardar el nombre de la carpeta de WordPress
WORDPRESS_FOLDER=$(tar -tf latest.tar.gz | head -1)

# Descomprimir WordPress en una carpeta con el nombre del cliente
CLIENT_NAME="MiCliente"
mkdir $CLIENT_NAME
tar -xvzf latest.tar.gz -C $CLIENT_NAME

# Configurar el virtual host
DOMAIN="mi-cliente.com"
SUBDOMAIN="blog"
VHOST_CONFIG="/etc/httpd/conf/vhosts/$DOMAIN.conf"
echo "<VirtualHost *:80>
ServerName $SUBDOMAIN.$DOMAIN
ServerAlias $SUBDOMAIN.$DOMAIN
DocumentRoot $PWD/$CLIENT_NAME/$WORDPRESS_FOLDER
</VirtualHost>" > $VHOST_CONFIG

# Reiniciar Apache
service httpd restart
