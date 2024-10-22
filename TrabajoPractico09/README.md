## Trabajo Práctico 9 - Implementación de Contenedores en Azure Parte 2

## Felipe Cañas

### Repo Azure

https://dev.azure.com/felipecanias/TP08

Use el mismo repo del TP08. El nombre del pipeline que use para este TP es TP09.

### Desarrollo:

### 4.1 Modificar nuestro pipeline para incluir el deploy en QA y PROD de Imagenes Docker en Servicio Azure App Services con Soporte para Contenedores

#### 4.1.1 - Agregar a nuestro pipeline una nueva etapa que dependa de nuestra etapa de Construcción y Pruebas y de la etapa de Construcción de Imagenes Docker y subida a ACR realizada en el TP08

Creamos el AppServicePlan:

![alt text](images/image.png)

Modificamos el pipeline:

![alt text](images/image-1.png)

![alt text](images/image-2.png)

![alt text](images/image-3.png)

![alt text](images/image-4.png)

### 4.2 Desafíos:
#### 4.2.1 Agregar tareas para generar Front en Azure App Service con Soporte para Contenedores

![alt text](images/image-5.png)

![alt text](images/image-6.png)

![alt text](images/image-7.png)

#### 4.2.2 Agregar variables necesarias para el funcionamiento de la nueva etapa considerando que debe haber 2 entornos QA y PROD para Back y Front.

![alt text](images/image-8.png)

#### 4.2.3 Agregar tareas para correr pruebas de integración en el entorno de QA de Back y Front creado en Azure App Services con Soporte para Contenedores.

![alt text](images/image-9.png)

#### 4.2.4 Agregar etapa que dependa de la etapa de Deploy en QA que genere un entorno de PROD.

![alt text](images/image-10.png)

![alt text](images/image-11.png)

![alt text](images/image-12.png)

![alt text](images/image-13.png)

![alt text](images/image-14.png)

![alt text](images/image-15.png)

![alt text](images/image-16.png)

#### 4.2.5 Entregar un pipeline que incluya:
- Etapa Construcción y Pruebas Unitarias y Code Coverage Back y Front
- Construcción de Imágenes Docker y subida a ACR
- Deploy Back y Front en QA con pruebas de integración para Azure Web Apps
- Deploy Back y Front en QA con pruebas de integración para ACI
- Deploy Back y Front en QA con pruebas de integración para Azure Web Apps con Soporte para contenedores
- Aprobación manual de QA para los puntos C,D,E
- Deploy Back y Front en PROD para Azure Web Apps
- Deploy Back y Front en PROD para ACI
- Deploy Back y Front en PROD para Azure Web Apps con Soporte para contenedores

El pipeline se llama "TP09 - Integrador"

![alt text](images/image-17.png)

![alt text](images/image-18.png)

![alt text](images/image-19.png)

![alt text](images/image-20.png)

![alt text](images/image-21.png)

![alt text](images/image-22.png)

![alt text](images/image-23.png)

![alt text](images/image-24.png)