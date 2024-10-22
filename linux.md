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

## Chmod Permission

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

