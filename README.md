#Magerun Docker Container

This provides a copy of [n98-magerun](https://github.com/netz98/n98-magerun) to be used in a docker environment.

#Usage

The container requires an environment variable called `MAGE_ROOT_DIR` to be defined.  This is passed to `magerun` through `--root-dir`.

The container also requires access to your Magento files, and access to the MySQL container.

##Docker Compose

Assuming you have a data container called `data` which contains your files that you mount to `/var/www/html`, and your MySQL container is called `db` then your `docker-compose.yml` might look something like this:

    magerun:
      image: meanbee/magerun
      environment:
        MAGE_ROOT_DIR: /var/www/html
      links:
        - db
      volumes_from:
        - data

This image can then be used to easily perform any `magerun` command, for example:

    docker-compose run magerun sys:setup:run    
    
