# PM2 Service

## Start a service

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

## Stop a service

```bash
pm2 stop 0
```

or 

```bash
pm2 stop MyService
```

## Show services

```bash
pm2 ls
```

## Reset your service IDs

```bash
pm2 save ## To Save your current pm2 instance
pm2 kill
pm2 resurrect
```