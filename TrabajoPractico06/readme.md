## Trabajo Práctico 6 - Pruebas Unitarias

### Desarrollo:

#### 4.2 Obtener nuestra App

A\. Clonar el repo https://github.com/ingsoft3ucc/Angular_WebAPINetCore8_CRUD_Sample.git

![alt text](./images/image.png)

B\. Seguir las instrucciones del README.md del repo clonado prestando atención a la modificación de la cadena de conexión en el appSettings.json para que apunte a la BD creada en 4.1

![alt text](./images/image-1.png)

![alt text](./images/image-2.png)

C\. Navegar a http://localhost:7150/swagger/index.html y probar uno de los controladores para verificar el correcto funcionamiento de la API.

![alt text](./images/image-4.png)

![alt text](./images/image-3.png)

D\. Navegar a http://localhost:4200 y verificar el correcto funcionamiento de nuestro front-end Angular

![alt text](./images/image-5.png)


#### 4.3 Crear Pruebas Unitarias para nuestra API

A\. En el directorio raiz de nuestro repo crear un nuevo proyecto de pruebas unitarias para nuestra API

![alt text](./images/image-6.png)

B\. Instalar dependencias necesarias

![alt text](./images/image-7.png)

C\. Editar archivo UnitTest1.cs reemplazando su contenido por

![alt text](./images/image-8.png)

D\. Renombrar archivo UnitTest1.cs por EmployeeControllerUnitTests.cs

![alt text](./images/image-9.png)

E\. Editar el archivo EmployeeCrudApi.Tests/EmployeeCrudApi.Tests.csproj para agregar una referencia a nuestro proyecto de EmployeeCrudApi reemplazando su contenido por

![alt text](./images/image-10.png)

F\. Ejecutar los siguientes comandos para ejecutar nuestras pruebas

```
dotnet build
dotnet test
```

G\. Verificar que se hayan ejecutado correctamente las pruebas

![alt text](./images/image-11.png)

H\. Verificar que no estamos usando una dependencia externa como la base de datos.


I\. Modificar la cadena de conexión en el archivo appsettings.json para que use un usuario o password incorrecto y recompilar el proyecto EmployeeCrudApi

![alt text](./images/image-12.png)

J\. Verificar que nuestro proyecto ya no tiene acceso a la BD navegando a http://localhost:7150/swagger/index.html y probando uno de los controladores:

![alt text](./images/image-15.png)

K\. En la carpeta de nuestro proyecto EmployeeCrudApi.Tests volver a correr las pruebas

L\. Verificar que se hayan ejecutado correctamente las pruebas inclusive sin tener acceso a la BD, lo que confirma que es efectivamente un conjunto de pruebas unitarias que no requieren de una dependencia externa para funcionar.

![alt text](./images/image-13.png)

M\. Modificar la cadena de conexión en el archivo appsettings.json para que use el usuario y password correcto y recompilar el proyecto EmployeeCrudApi

![alt text](./images/image-16.png)

![alt text](./images/image-17.png)

N\. Verificar que nuestro proyecto vuelve a tener acceso a la BD navegando a http://localhost:7150/swagger/index.html y probando uno de los controladores:

![alt text](./images/image-18.png)

#### 4.4 Creamos pruebas unitarias para nuestro front de Angular:

A\. Nos posicionamos en nuestro proyecto de front, en el directorio EmployeeCrudAngular/src/app

![alt text](./images/image-19.png)

B\. Editamos el archivo app.component.spec.ts reemplazando su contenido por:

![alt text](./images/image-20.png)

C\. Creamos el archivo employee.service.spec.ts reemplazando su contenido por:

![alt text](./images/image-21.png)

D\. Editamos el archivo employee.component.spec.ts ubicado en la carpeta **employee** reemplazando su contenido por:

![alt text](./images/image-22.png)

E\. Editamos el archivo addemployee.component.spec.ts ubicado en la carpeta **addemployee** reemplazando su contenido por:

![alt text](./images/image-23.png)

F\. En el directorio raiz de nuestro proyecto EmployeeCrudAngular ejecutamos el comando

G\. Vemos que se abre una ventana de Karma con Jasmine en la que nos indica que los tests se ejecutaron correctamente

![alt text](./images/image-25.png)

H\. Vemos que los tests se ejecutaron correctamente:

![alt text](./images/image-24.png)

I\. Verificamos que no esté corriendo nuestra API navegando a http://localhost:7150/swagger/index.html y recibiendo esta salida:

![alt text](./images/image-26.png)

J\. Los puntos G y H nos indican que se han ejecutado correctamente las pruebas inclusive sin tener acceso a la API, lo que confirma que es efectivamente un conjunto de pruebas unitarias que no requieres de una dependencia externa para funcionar.

#### 4.5 Agregamos generación de reporte XML de nuestras pruebas de front.

A\. Instalamos dependencia karma-junit-reporter

![alt text](./images/image-27.png)

B\. En el directorio raiz de nuestro proyecto (al mismo nivel que el archivo angular.json) creamos un archivo karma.conf.js con el siguiente contenido

![alt text](./images/image-28.png)

C\. Ejecutamos nuestros test de la siguiente manera:

![alt text](./images/image-29.png)

D\. Verificamos que se creo un archivo test-result.xml en el directorio test-results que está al mismo nivel que el directorio src

![alt text](./images/image-30.png)

#### 4.6 Modificamos el código de nuestra API y creamos nuevas pruebas unitarias:

A\. Realizar al menos 5 de las siguientes modificaciones sugeridas al código de la API:

- La longitud máxima del nombre y apellido del empleado debe ser de 100 caracteres.
- Asegurar que el nombre del empleado no contenga caracteres especiales o números, a menos que sea necesario (por ejemplo, caracteres especiales en apellidos como "O'Connor" o "García").
- Validar que el nombre tenga un número mínimo de caracteres, por ejemplo, al menos dos caracteres para evitar entradas inválidas como "A".
- Verificar que el nombre no contenga números, ya que no es común en los nombres de empleados.
- Evitar que se ingresen caracteres repetidos de forma excesiva, como "Juuuuaannnn".

![alt text](./images/image-31.png)

B\. Crear las pruebas unitarias necesarias para validar las modificaciones realizadas en el código

![alt text](./images/image-32.png)

![alt text](./images/image-33.png)

![alt text](./images/image-34.png)

![alt text](./images/image-35.png)

#### 4.7 Modificamos el código de nuestro Front y creamos nuevas pruebas unitarias:

A\. Realizar en el código del front las mismas modificaciones hechas a la API.

![alt text](./images/image-41.png)

B\. Las validaciones deben ser realizadas en el front sin llegar a la API, y deben ser mostradas en un toast como por ejemplo https://stackblitz.com/edit/angular12-toastr?file=src%2Fapp%2Fapp.component.ts o https://stackblitz.com/edit/angular-error-toast?file=src%2Fapp%2Fcore%2Frxjsops.ts


![alt text](./images/image-36.png)

![alt text](./images/image-37.png)

![alt text](./images/image-38.png)

![alt text](./images/image-39.png)

![alt text](./images/image-40.png)

C\. Crear las pruebas unitarias necesarias en el front para validar las modificaciones realizadas en el código del front.

![alt text](./images/image-42.png)

![alt text](./images/image-43.png)

#### 6. Subir el proyecto

Link repositorio: https://github.com/felipecanias/Angular_WebAPINetCore8_CRUD_Sample
