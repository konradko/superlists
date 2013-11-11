Provisioning a new site
=======================

## Required packages:

* nginx
* Python 3
* Git
* pip
* virtualenv

eg, on Ubuntu:

    sudo apt-get install nginx git python3 python3-pip
    sudo pip-3.3 install virtualenv

## Nginx Virtual Host config

* see nginx.template.conf
* replace SITENAME with, eg, staging.my-domain.com

## Upstart Job

* see gunicorn-upstart.template.conf
* replace SITENAME with, eg, staging.my-domain.com

    sudo ln -s ../sites-available/lists.korzel.com \
        /etc/nginx/sites-enabled/lists.korzel.com

    sed "s/SITENAME/lists.korzel.com/g" deploy_tools/gunicorn-upstart-template.conf | \
        sudo tee /etc/init/lists.korzel.com.conf

    sudo ln -s ../sites-available/lists-staging.korzel.com \
        /etc/nginx/sites-enabled/lists-staging.korzel.com

    sed "s/SITENAME/lists-staging.korzel.com/g" deploy_tools/gunicorn-upstart-template.conf | \
        sudo tee /etc/init/lists-staging.korzel.com.conf

    sudo service nginx reload
    sudo restart gunicorn-lists.korzel.com
    sudo restart gunicorn-lists-staging.korzel.com

## Folder structure:
Assume we have a user account at /home/username

/home/username
└── sites
    └── SITENAME
         ├── database
         ├── source
         ├── static
         └── virtualenv