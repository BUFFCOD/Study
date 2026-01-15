# Using Web Services on RHEL

Two web services are commonly used on RHEL:

Apache (httpd) has been around for a long time.
    it offers many features that are implemented by using modueles

Nginx is a smaller lightweight webserver.

It is commonly used when web services need to be containerized

It is simpler than Apache but also faster

## Exploring HTTP Configuration

The main httpd configuration file is /etc/httpd/conf/httpd.conf.

additional drop in files can be stored in /etc/httpd/conf.d/.

The default DocumentRoot is /var/www/htdocs

Apache looks for a file with the name index.html in this directory.

Other files or directories that copied into the DocumentRoot will be presented by the Apache server.

## Creating a Basic WebSite