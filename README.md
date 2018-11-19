# DevOpsTechnicalChallenge
#Installs nginx, Apache, PHP 7 and mod_php
#Create 2 bind volumes. One for each document root (Apache & Nginx).

Nginx configuration:
 1. nginx to run on port 80
 2. configure nginx to serve static files from Document root which
has already been mounted as a docker bind volume
 3. add miscellaneous files to test with for Document root to the
directory used as the docker bind volume
 4. reverse proxy files that are not a css, jpg, png or js file to
Apache on port 8080


Apache configuration:
 1. Listens on port 8080 and uses a default virtual host
 2. create a URL rewrite rule that redirects all requests that do
not have the X-Forwarded-Proto header set to https to redirect to an
https version of that URL
 3. Using a LocationMatch directive, protect the URL pattern,
"/protected" with basic authentication; provide credentials
 4. For files with a eot,ttf,otf,woff and woff2 extensions, create a
configuration that enables CORS and allows the OPTIONS method
 5. A phpinfo test page should exist in the Document root mounted as
a bind volume
Part 2: Assume a Centos 7 OS, use Ansible to perform the same tasks as
done by Docker
 1. create 3 roles (Apache, Nginx, PHP) and a playbook with those
roles
 2. a localhost inventory file
 3. use web server config templates
 4. tasks should be able to be run by tag name
