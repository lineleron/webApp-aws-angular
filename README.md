# Blockstellart Bootcamp
Este proyecto fue generado con [Angular CLI](https://github.com/angular/angular-cli) versión 15.0.0. para el Bootcamp de AWS de **Lino Ele Bengono*

## Servidor de desarrollo
Ejecuta `ng serve` para un servidor de desarrollo. Navega a `http://localhost:4200/`. La aplicación se recargará automáticamente si cambias alguno de los archivos fuente.  

## Andamiaje de código
Ejecute `ng generate component component-name` para generar un nuevo componente. También puedes usar `ng generate directive|pipe|service|class|guard|interface|enum|module`.  

## Construir
Ejecute `ng build` para construir el proyecto. Los artefactos de construcción se almacenarán en el directorio `dist/`.  

## Ejecutar pruebas unitarias
Ejecuta `ng test` para ejecutar las pruebas unitarias a través de [Karma](https://karma-runner.github.io).  

## Ejecutar pruebas end-to-end
Ejecute `ng e2e` para ejecutar las pruebas de extremo a extremo a través de una plataforma de su elección. Para utilizar este comando, primero necesitas añadir un paquete que implemente capacidades de pruebas de extremo a extremo.  

## Más ayuda
Para obtener más ayuda sobre la CLI de Angular usa `ng help` o visita la página [Angular CLI Overview and Command Reference](https://angular.io/cli).  

## Instrucciones Angular
1. Abra la linea de comandos en VS Code con ```ctrl+ñ o cmd + ñ``` o editor de codigo preferido.
**Nota**: Asegurese de estar al nivel del archivo *angular.json*, de lo contrario el siguiente comando podría no ser reconocido.
2. Ejecute `ng build` para construir el proyecto. Los archivos se almacenarán en el directorio `dist/`.
3. Espere a que el proceso de build concluya, navegue a la carpeta dist y copie el contenido que se encuentra dentro de esta carpeta. Ya que S3 buscara el archivo index.html.
3. Copie los archivos al bucket S3, de forma manual o utilizando el siguiente comando: ```aws s3 sync dist/blockstellart-bootcamp/ s3://blockstellart-bootcamp-website/ ```

## Instrucciones S3
[Configuración de un sitio web estático en Amazon S3](https://docs.aws.amazon.com/es_es/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html#step7-test-web-site).  


## Instrucciones Docker

### Nginx Config para Angular
El archivo _nginx.conf_ muestra la configuración de Nginx para nuestra aplicación Angular. Configurado en la carpeta raíz para Nginx y evita errores 404 Not Found estableciendo el archivo por defecto en la página base de la aplicación Angular(/index.html).  

### Dockerfile
Un Dockerfile define todas las instrucciones utilizadas para construir una imagen Docker. El siguiente Dockerfile construye una imagen de nuestra aplicación Angular ejecutándose en Nginx, utiliza una construcción multietapa incluyendo múltiples sentencias FROM. Cada declaración FROM comienza una nueva etapa de construcción a partir de la imagen base especificada (por ejemplo, nginx), reduciendo significativamente el tamaño de la imagen final.  

### Archivo .dockerignore
Un archivo . dockerignore funciona igual que un archivo .gitignore pero para rutas/patrones que quieras excluir de tu imagen Docker construida.  

### Creación de imagen Docker para aplicación Angular en Nginx
Ejecute el siguiente comando desde la carpeta raíz de la aplicación Angular (donde se encuentra el archivo Docker ). Se creará una nueva imagen Docker con la etiqueta blockstellart-ws.  


```
docker build -t blockstellart-ws .
```  


### Ejecutar contenedor Docker con Angular App en Nginx
Ejecute el siguiente comando para crear e iniciar un nuevo contenedor Docker desde la imagen blockstellart-ws y publícalo en el puerto 8080 del equipo local.  

```
docker run --name bootcamp-ws -dp 8080:80 blockstellart-ws
```  

### Aplicación Angular en el navegador
Abra la aplicación Angular que se ejecuta en Docker con Nginx en la URL http://localhost:8080.  