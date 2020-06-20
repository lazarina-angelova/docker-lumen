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
$ git clone https://github.com/lazarina-angelova/docker-lumen
```

```bash
cp /path/to/docker-lumen/.env.example /path/to/docker-lumen/.env
```

### 3. Start containers
```bash
cd /path/to/docker-lumen && docker-compose up -d
```

### 4. Install backend requirements (change the name of the Docker container if you have changed the PROJECT_NAME in the .env file)
```bash
docker exec -u 1000 app-php ash -c "cd /app && composer install --no-ansi -o -n"
```

### 5. Run DB setup

#### 6.1. Generate new migration
```bash
docker exec -u 1000 app-php ash -c "cd /app && php artisan doctrine:migrations:generate"
```

#### 6.2. Run migrations
```bash
docker exec -u 1000 app-php ash -c "cd /app && php artisan migrate"
```

#### 6.3. Generate Repositories
```bash
docker exec -u 1000 app-php ash -c "cd /app && php artisan make:entity --regenerate"
```

### 6. Edit your hosts file to include the following row
`127.0.0.1 localhost`

### 7. Go to  (change the name of the port if you have changed the HTTP_PORT in the .env file)
http://localhost
