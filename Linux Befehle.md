# Linux Befehle
## User anlegen
```
useradd [name]
```
## User passwort ändern
```
passwd [user]
```

## Group erstellen

```
groupadd [Gruppe]
```

## Group an user verteilen
### Als weitere Gruppe
```
usermod -a -G [Gruppe] [User]
```

### Als standard Gruppe
```
usermod -g [Gruppe] [User]
```

## Anzeigen von Gruppen eines Users
```
groups [User]
```

## Erstellen einer Datei
```
touch [name]
```

## Ändern des Owners (Gruppe) von Ordnern und Unterordnern

```
chown -R [User]:[Gruppe] [Ordner]
```

## Ändern der Permissions von Ordnern und Unterordnern

```
chmod [ID] -R [Gruppe]
```

Mit ID ist die PermissionID gemeint, siehe [hier](https://chmod-calculator.com/).


## Einloggen als User
```
su [User]
```


## Moven von Ordnern in einen anderen Ordner
```
move [Ordner der gemoved werden soll] [Zielordner]
```

## Anzeigen des aktuellen Parent Ordners
```
pwd
```

## Anlegen des Public SSH Keys für einen User
Im root folder des Users Ordner `.ssh` erstellen.\
Darin die Datei `authorized_keys` erstellen.\
Mit vim bearbeiten und den Public-Key reinpasten.

## Chmod Permission Rechte

```
rwxrwxrwx
```
r -> read\
w -> write\
x -> execute

1. Owner
2. Group
3. Public