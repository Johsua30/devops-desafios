# Despliegue en Kubernetes

Clonar el repositorio https://github.com/Johsua30/devops-desafios.git a nuestra PC.

- Crear la imagen de Docker
` docker build -t mtg-wishlist-app:1.0 . `

- Desplegar en kubernetes
` kubectl apply -f deployment.yaml `
` kubectl apply -f service.yaml `

- Verificar que el pod esté corriendo
` kubectl get pods `

- Acceder a la aplicación
Ingresar desde el navegador a ` localhost:30001 `

- Eliminar todo
` kubectl delete -f service.yaml `
` kubectl delete -f deployment.yaml `