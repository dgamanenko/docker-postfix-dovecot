# Postfix with dovecot into docker

##Create email addresses:
 Use MySQL DB with [tables](https://github.com/dgamanenko/docker-postfix-dovecot/blob/master/mailschema.sql); add email domains into `mail_virtual_domains`, add email users to `mail_virtual_users`. 

## pull from DockerHub

```
docker pull dmtr/docker-postfix-dovecot
```

## Docker build

```
docker build -t postfix .  
```

## docker run

```
docker run -i -t -e APP_HOST=example.com -e DB_NAME=dbname -p 25:25 -p 110:110 -p 143:143 -p 995:995 -p 587:587 -v /var/run/mysqld/:/var/run/mysqld -v /home/vmail:/home/vmail/ postfix
```

### Environment variables

* **APP_HOST** (required)- email server host
* **DB_NAME** (required) - database
* **DB_USER** (root) - user to access mysql database
* **DB_PASSWORD** - mysql user password

### Directories

* `/var/run/mysqld/:/var/run/mysqld/` - MySQL socket
* `/home/vmail/:/home/vmail/` - directory to store emails
