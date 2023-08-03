# Linux Befehle
## User anlegen
```bash
useradd [name]
```
## User passwort ändern
```bash
passwd [user]
```

## Group erstellen

```bash
groupadd [Gruppe]
```

## Group an user verteilen
### Als weitere Gruppe
```bash
usermod -a -G [Gruppe] [User]
```

### Als standard Gruppe
```bash
usermod -g [Gruppe] [User]
```

## Anzeigen von Gruppen eines Users
```bash
groups [User]
```

## Erstellen einer Datei
```bash
touch [name]
```

## Ändern des Owners (Gruppe) von Ordnern und Unterordnern

```bash
chown -R [User]:[Gruppe] [Ordner]
```

## Ändern der Permissions von Ordnern und Unterordnern

```bash
chmod [ID] -R [Gruppe]
```

Mit ID ist die PermissionID gemeint, siehe [hier](https://chmod-calculator.com/).


## Einloggen als User
```bash
su [User]
```


## Moven von Ordnern in einen anderen Ordner
```bash
move [Ordner der gemoved werden soll] [Zielordner]
```

## Anzeigen des aktuellen Parent Ordners
```bash
pwd
```

## Anlegen des Public SSH Keys für einen User
Im root folder des Users Ordner `.ssh` erstellen.\
Darin die Datei `authorized_keys` erstellen.\
Mit vim bearbeiten und den Public-Key reinpasten.

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

Information from (here)[https://fixyacloud.wordpress.com/2020/01/26/how-to-run-a-server-on-port-80-as-a-normal-user-on-linux/]


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