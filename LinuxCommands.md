# Linux Commands
## User
### Create User
```bash
useradd myUser
```
### Change user password
```bash
passwd myUser
```

### Delete user

```bash
userdel myUser
```

## Groups

### Create group
```bash
groupadd myGroup
```

### Delete group
```bash
groupdel myGroup
```

### Add user to group

```bash
usermod -a -G myGroup myUser
```

### Set standard group for a user
```bash
usermod -g myGroup myUser
```

### Show a user's groups
```bash
groups myUser
```

## Create a file
```bash
touch myFile
```

## Directory/File modification

### Change owner of a directory/file
```bash
chown -R myUser:myUsersGroup myFileOrDirectory
```

### Change permission of directory or file

```bash
chmod 777 -R myDirOrFile
```
* -R for every child directory/file
* 777 is the permissionId, see [here](https://chmod-calculator.com/).


## Log in as another user (superuser)
```bash
su [User]
```

## Change bash from a user
```bash
chsh -s /bin/bash [username]
```

## Set to "no password required"

```bash
passwd -d [username]
```

## Move files/directories
```bash
move /path/to/oldFileOrFolder /path/to/newFolder
```

## Show current parent dir
```bash
pwd
```

## Create SSH for another user
1. Create `.ssh` folder in the home dir of the user. \
2. Create `authorized_keys` in /.ssh \
3. Add the public key to `authorized_keys`

## Chmod Permission Rechte

```bash
rwxrwxrwx
```
r -> read\
w -> write\
x -> execute

1. Owner
2. Group
3. Public

## Port redirection

### Which ports are used from the user ports

```bash
netstat -tuln | grep -E ':[1-9][0-9]{3,4}\s'
```

### Redirect from port 80 to 8080

```bash
iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
```

### Show rules
```bash
iptables -t nat --line-numbers -n -L
```

### Delete a rule
```bash
iptables -t nat -D PREROUTING 2
```

Information from [here](https://fixyacloud.wordpress.com/2020/01/26/how-to-run-a-server-on-port-80-as-a-normal-user-on-linux/)


## PM2 Service

### Start a service

```bash
pm2 start index.js --name MyNewService
```

or

```bash
pm2 start ecosystem.config.js
```

With a file like this:

```js
// ecosystem.config.js File
module.exports = {
    apps: [{
        name: "MyNewService",
        script: "./index.js",
        error_file: "./--error",
        out_file: './out.log',
        log_date_format: 'YYYY-MM-DD HH:mm:ss:SSS',
        cwd: "./" // Path to directory where package.json is located
    }]
}

```

### Stop a service

```bash
pm2 stop 0
```

or 

```bash
pm2 stop MyService
```

### Show services

```bash
pm2 ls
```

### Reset your service IDs

```bash
pm2 save ## To Save your current pm2 instance
pm2 kill
pm2 resurrect
```

## Change welcome screen

Create custom file
```bash
cd /etc/update-motd.d/
ls
touch 99-custom-welcome
nano 99-custom-welcome
```

Check permissions for everything in a folder
```bash
ls -l /etc/update-motd.d/
```

Give execute permissions to everything in a folder
```bash
sudo chmod +x /etc/update-motd.d/*
```

## Setup nginx

### Install
```bash
sudo apt install nginx
```

### Commands

```bash
sudo systemctl stop nginx
sudo systemctl start nginx
sudo systemctl restart nginx
sudo systemctl reload nginx
# Startup
sudo systemctl disable nginx
sudo systemctl enable nginx
```

### Configuration

Create file here
`/etc/nginx/sites-available/my-domain`

Edit file
```bash
server {  
    listen 80;
    server_name www.my-domain my-domain;
    location / {  
            proxy_pass http://localhost:8080;  
            proxy_http_version 1.1;  
            proxy_set_header Upgrade $http_upgrade;  
            proxy_set_header Connection 'upgrade';  
            proxy_set_header Host $host;  
            proxy_cache_bypass $http_upgrade;  
    }  
}
```


Link file
```bash
sudo ln -s /etc/nginx/sites-available/my-domain /etc/nginx/sites-enabled/
```


### Get Let's Encrypt certificate for domain by using nginx plugin

Download plugin
```bash
sudo apt install certbot python3-certbot-nginx
```

Get certificate for YOUR-DOMAIN.com
```bash
sudo certbot --nginx -d YOUR-DOMAIN.com -d www.YOUR-DOMAIN.com
```

Create auto-renewal because certificate is only available for 90 days.
```bash
sudo certbot renew --dry-run
```

## Docker

### Create an image

```bash
docker build --platform [linux/amd64|linux/arm64] -t NAME_OF_IMAGE .
```

### Inspect to get information about the image

```bash
docker inspect NAME_OF_IMAGE
```

### Tag to push to hub

```bash
docker tag NAME_OF_IMAGE:TAG USERNAME/NAME_OF_REPOSITORY:TAG
```

### Pull from hub

```bash
docker pull USERNAME/NAME_OF_REPOSITORY
```

### Run container in background

```bash
docker run -d -p 3200:3000 USERNAME/NAME_OF_REPOSITORY
```

### More

```bash
docker ps # See containers
docker images # See images
```
