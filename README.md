dockerfiles-centos7-nginx
========================

CentOS 7 Dockerfile for nginx, This build of nginx listens on port 8080 by default. Please be aware of this
when you launch the container.

error_log and access_log will go to STDOUT.


To build:

Copy the sources down -

    # docker build --rm --tag <username>/nginx:centos7 .

To run:

    # docker run -d -p 80:8080 <username>/nginx:centos7

To test:

    # curl http://localhost

DevOpsTechnicalChallenge

#Installs nginx, Apache, PHP 7 and mod_php #Create 2 bind volumes. One for each document root (Apache & Nginx).

Nginx configuration:

    nginx to run on port 80
    configure nginx to serve static files from Document root which has already been mounted as a docker bind volume
    add miscellaneous files to test with for Document root to the directory used as the docker bind volume
    reverse proxy files that are not a css, jpg, png or js file to Apache on port 8080

Apache configuration:

    Listens on port 8080 and uses a default virtual host
    create a URL rewrite rule that redirects all requests that do not have the X-Forwarded-Proto header set to https to redirect to an https version of that URL
    Using a LocationMatch directive, protect the URL pattern, "/protected" with basic authentication; provide credentials
    For files with a eot,ttf,otf,woff and woff2 extensions, create a configuration that enables CORS and allows the OPTIONS method
    A phpinfo test page should exist in the Document root mounted as a bind volume Part 2: Assume a Centos 7 OS, use Ansible to perform the same tasks as done by Docker
    create 3 roles (Apache, Nginx, PHP) and a playbook with those roles
    a localhost inventory file
    use web server config templates
    tasks should be able to be run by tag name


Commands to build the docker:
============================

docker build -t "nginx:dockerfile" .
