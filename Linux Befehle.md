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