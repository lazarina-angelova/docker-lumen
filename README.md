# Steps to create dev environment

### 1. Install Docker

#### 1.1 Windows
- [Docker for Windows (stable)](https://docs.docker.com/docker-for-windows/install/#download-docker-for-windows)


#### 1.2 Linux
- git
- docker (more info [here](https://docs.docker.com/engine/installation/))
- docker-compose (more info [here](https://docs.docker.com/compose/install/#install-as-a-container))

#### 1.3 
- [Docker for Mac](https://docs.docker.com/docker-for-mac/install/)


### 2. Clone the repo and create environment file
```bash
$ git clone https://github.com/lazarina-angelova/myapp
```

```bash
cp /path/to/myapp/.env.example /path/to/myapp/.env
```

### 3. Start containers
```bash
cd /path/to/myapp && docker-compose up -d
```

### 4. Install backend requirements (change the name of the Docker container if you have changed the APP_NAME in the .env file)
```bash
docker exec -u 1000 myapp-php bash -c "cd /app && composer install --no-ansi -o -n"
```

### 5. Run DB setup

#### 56.1. Create new migration
```bash
docker exec -u 1000 myapp-php bash -c "cd /app && php artisan make:migration {Migration Name}"
```

#### 5.1. Run migrations
```bash
docker exec -u 1000 myapp-php bash -c "cd /app && php artisan migrate --force"
```

### 6. Edit your hosts file to include the following row
`127.0.0.1 localhost`

### 7. Go to http://localhost
