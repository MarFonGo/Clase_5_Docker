# Proyecto Nginx con Docker

En este proyecto, vamos a crear una imagen de Docker personalizada basada en Nginx, utilizando un archivo Dockerfile. Luego, vamos a levantar un contenedor con esa imagen utilizando Docker Compose y finalmente subir los archivos al repositorio en GitHub.

## Pre-requisitos

- Máquina virtual Ubuntu sin Docker instalado.

## Pasos

### 1. Instalar Docker en Ubuntu

Ejecuta los siguientes comandos para instalar Docker en la máquina virtual Ubuntu:

```bash
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

### 2. Crear el directorio del proyecto y los archivos necesarios

Crea un directorio para el proyecto y coloca allí los archivos "Dockerfile" y "index.html":

```bash
mkdir proyecto
cd proyecto
```

### 3. Crear el archivo Dockerfile

Abre el archivo "Dockerfile" y escribe el siguiente contenido:

```Dockerfile
FROM nginx
COPY index.html /usr/share/nginx/html
```

Guarda y cierra el archivo:

```bash
nano Dockerfile
```

### 4. Crear el archivo docker-compose.yml

Abre el archivo "docker-compose.yml" y escribe el siguiente contenido:

```yaml
version: '3'
services:
  web:
    build: .
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
      - ./logs:/var/log/nginx
      - ./html:/usr/share/nginx/html
    restart: always
```

Guarda y cierra el archivo:

```bash
nano docker-compose.yml
```

### 5. Crear el archivo nginx.conf

Abre el archivo "nginx.conf" y escribe el siguiente contenido:

```nginx
worker_processes  1;
events {
    worker_connections  1024;
}
http {
    server {
        listen 80;
        server_name localhost;
        location / {
            root /usr/share/nginx/html;
            index index.html;
        }
    }
    access_log /var/log/nginx/access.log;
    error_log /var/log/nginx/error.log;
}
```

Guarda y cierra el archivo:

```bash
nano nginx.conf
```

### 6. Crear el archivo index.html

Crea el archivo "index.html" con el contenido que desees:

```bash
nano index.html
```

### 7. Crear el archivo Readme.md

Crea el archivo "Readme.md" con los pasos seguidos:

```bash
nano Readme.md
```

### 8. Crear el directorio logs

Crea el directorio "logs" en el directorio del proyecto:

```bash
mkdir logs
```

### 9. Construir la imagen de Docker

Ejecuta el siguiente comando para construir la imagen de Docker:

```bash
docker build -t mi_nginx .
```

### 10. Levantar el contenedor con Docker Compose

Ejecuta el siguiente comando para levantar el contenedor con Docker Compose:

```bash
docker-compose up -d
```

### 11. Verificar el funcionamiento del contenedor

Abre un navegador web y accede a la dirección "http://localhost". Deberías ver la página web personalizada que definiste en el archivo "index.html".

### 12. Subir archivos al repositorio en GitHub

Sube los archivos al repositorio en GitHub utilizando los comandos "git add", "git commit" y "git push":

```bash
git init
git add .
git commit -m "Primer commit del proyecto Nginx con Docker"
git remote add origin <URL del repositorio en GitHub>
git push -u origin main
```

## Resumen

Con estos pasos, hemos creado una imagen de Docker basada en Nginx, creado un Docker Compose para levantar un contenedor con esa imagen y subido los archivos a GitHub en una máquina virtual Ubuntu que no tenía Docker
