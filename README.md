<!-- Sistemas Operativos 2 -->
## Sistemas Operativos 2

### Proyecto final

Definición y ejecución de imagen personalizada sobre ambiente Kubernetes. 

### Prerequisitos
Tener previamente instalado microk8s, usar este tutorial <a href="https://microk8s.io/docs/getting-started">MicroK8s - Get started</a>

### Creacion de imagen custom
Construir una imagen custom con el nombre "mynginx" usando como base la imagen oficial de nginx y copiando el folder html a la ubicacion /usr/share/nginx/html (usando el archivo Dockerfile).
  ```sh
  docker build . -t mynginx
  ```

### Exportar la imagen custom
La imagen previamente contruida se exporta a al archivo con el nombre "myimage.tar".
  ```sh
  docker save mynginx > myimage.tar
  ```
  
### Importar la imagen custom a Microk8s 
La imagen que esta contenida en el archivo "myimage.tar" se debe importar a Microk8s.
  ```sh
  microk8s ctr image import myimage.tar
  ```
  
### Crear un deployment/bot con la imagen mynginx
Crear un deployment/bot usando la imagen cargada del archivo "myimage.tar", usando el archivo mynginx.yml.
  ```sh
  microk8s kubectl apply -f myngix.yml
  ```
  
### Exponer el deployment/bot 
Exponer el deployment/bot.
  ```sh
  microk8s kubectl expose deployment nginx-deployment --type=NodePort --port=80 --name=nginx-service
  ```
