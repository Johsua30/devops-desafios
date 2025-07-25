# Correr la aplicación con Jenkins

Primero se debe correr Jenkins desde un contenedor y configurarlo.

### Ejecutar jenkin para usar Docker del Host

` docker run -p 8080:8080 -p 50000:50000 -d --name jenkinsv1 -v /var/run/docker.sock:/var/run/docker.sock -v jenkins_home:/var/jenkins_home  --restart=always jenkins/jenkins:alpine `

### Conectarse al contenedor con usuario root

` docker exec -it --user root jenkinsv1 sh `

### Instalar Docker en Jenkins

` apk update `
` apk add docker-cli `

### Validar grupo Docker

` ls -l /var/run/docker.sock `

Veremos algo similar : srw-rw---- 1 root root 0 Jun 27 20:04 /var/run/docker.sock

### Crear grupo Docker y agregar usuario Jenkins al grupo Docker

- ` addgroup docker `
- ` addgroup jenkins docker `
- ` chgrp docker /var/run/docker.sock `
- ` chmod 660 /var/run/docker.sock `
presionar Ctrl+c
- ` docker restart jenkinsv1 `

### Ingresar a Jenkins

Ingresar a localhost:8080 desde un navegador y seguir los pasos iniciales.

### Configurar credenciales de DockerHub

- En Jenkins, ir a `Manage Jenkins` > `Credentials`.
- Seleccionar el domain `(global)` y hacer clic en `Add Credentials`.
- Elegir `Username with password` y scope `Global`.
- En `Username`, ingresar su ID de Docker Hub.
- En `Password`, ingresar su contraseña.
- En `ID`, ingresar `dockerhub_id`.

### Crear y ejecutar el pipeline

- En Jenkins hacer click en `New Item`.
- Darle un nombre al pipeline(Ejemplo, wishlist-app).
- Seleccionar `Pipeline` y luego `OK`.
- Bajar a la sección de `Pipeline`.
- Seleccionar `Pipeline script from SCM` y en SCM elegir `Git`.
- En `Repository URL` ingresar https://github.com/Johsua30/devops-desafios
- En `Branch specifier` ingresar */main

- Para ejecutar el pipeline ingresar en el mismo y hacer click en `Build Now`

### Probar la imagen

Correr el comando ``` docker run --name wishlist-app -d -p 8085:80 johsua30/mtg-wishlist-app ```
Ingresar a localhost:8085

