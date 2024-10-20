## Trabajo Práctico 8 - Implementación de Contenedores en Azure y Automatización con Azure CLI

## Felipe Cañas

### Desarrollo:

#### Prerequisitos:

Azure CLI instalado

![alt text](images/image.png)

### 4.1 Modificar nuestro pipeline para construir imágenes Docker de back y front y subirlas a ACR
#### 4.1.1 Crear archivos DockerFile para nuestros proyectos de Back y Front
En la raiz de nuestro repo crear una carpeta docker con dos subcarpetas api y front, dentro de cada una de ellas colocar los dockerfiles correspondientes para la creación de imágenes docker en función de la salida de nuestra etapa de Build y Test.

![alt text](images/image-1.png)

#### 4.1.2 Crear un recurso ACR en Azure Portal siguiendo el instructivo 5.1

![alt text](images/image-2.png)

#### 4.1.3 Modificar nuestro pipeline en la etapa de Build y Test

 - Backend:

 ![alt text](images/image-3.png)

 - Frontend:

 ![alt text](images/image-4.png)

#### 4.1.4 En caso de no contar en nuestro proyecto con una ServiceConnection a Azure Portal para el manejo de recursos, agregar una service connection a Azure Resource Manager como se indica en instructivo 5.2

![alt text](images/image-5.png)

#### 4.1.5 Agregar a nuestro pipeline variables

![alt text](images/image-6.png)

#### 4.1.6 Agregar a nuestro pipeline una nueva etapa que dependa de nuestra etapa de Build y Test

![alt text](images/image-7.png)

#### 4.1.7 - Ejecutar el pipeline y en Azure Portal acceder a la opción Repositorios de nuestro recurso Azure Container Registry. Verificar que exista una imagen con el nombre especificado en la variable backImageName asignada en nuestro pipeline

![alt text](images/image-8.png)

![alt text](images/image-9.png)

#### 4.1.8 - Agregar tareas para generar imagen Docker de Front (DESAFIO)

![alt text](images/image-10.png)

![alt text](images/image-11.png)

#### 4.1.9 - Agregar a nuestro pipeline una nueva etapa que dependa de nuestra etapa de Construcción de Imagenes Docker y subida a ACR
 - Agregar variables a nuestro pipeline:

 ![alt text](images/image-14.png)

 - Agregar variable secreta cnn-string-qa desde la GUI de ADO que apunte a nuestra BD de SQL Server de QA como se indica en el instructivo 5.3

![alt text](images/image-12.png)

![alt text](images/image-13.png)

 - Agregar tareas para crear un recurso Azure Container Instances que levante un contenedor con nuestra imagen de back

 ![alt text](images/image-15.png)

#### 4.1.10 - Ejecutar el pipeline y en Azure Portal acceder al recurso de Azure Container Instances creado. Copiar la url del contenedor y navegarlo desde browser. Verificar que traiga datos.

![alt text](images/image-16.png)

![alt text](images/image-17.png)

![alt text](images/image-18.png)

#### 4.1.11 - Agregar tareas para generar un recurso Azure Container Instances que levante un contenedor con nuestra imagen de front (DESAFIO)

![alt text](images/image-19.png)

![alt text](images/image-20.png)

![alt text](images/image-21.png)

![alt text](images/image-22.png)

#### 4.1.12 - Agregar tareas para correr pruebas de integración en el entorno de QA de Back y Front creado en ACI.

![alt text](images/image-23.png)

![alt text](images/image-24.png)

### 4.2 Desafíos:
#### 4.2.1 Agregar tareas para generar imagen Docker de Front. (Punto 4.1.8)
*Completado*
#### 4.2.2 Agregar tareas para generar en Azure Container Instances un contenedor de imagen Docker de Front. (Punto 4.1.11)
*Completado*
#### 4.2.3 Agregar tareas para correr pruebas de integración en el entorno de QA de Back y Front creado en ACI. (Punto 4.1.12)
*Completado*
#### 4.2.4 Agregar etapa que dependa de la etapa de Deploy en ACI QA y genere contenedores en ACI para entorno de PROD.

![alt text](images/image-25.png)

![alt text](images/image-26.png)

![alt text](images/image-27.png)

![alt text](images/image-28.png)

![alt text](images/image-29.png)

![alt text](images/image-30.png)

![alt text](images/image-31.png)

![alt text](images/image-32.png)