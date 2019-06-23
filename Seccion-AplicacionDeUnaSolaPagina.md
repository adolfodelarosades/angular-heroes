# Aplicación 2: Aplicación de una sola página (SPA)

## Contenido

:+1:

## Introducción a la sección

:+1:

## ¿Qué veremos en esta sección? 							

:+1:

## Demostración de lo que lograremos en esta sección

:open_mouth:

## Iniciar el proyecto - SPA

1. Crear proyecto angular

    `ng new heroes`

2. Arrancar proyecto

    `cd heroes`

    `ng serve -o`

3. Cargar proyecto en el navegador

    `http://localhost:4200/`

4. Configurar Git en el proyecto (Creo que esto se creó solo)

    `git init`

5. Crear repositorio remoto

    Ir a [GitHub](https://github.com) y crear el repositorio **angular-heroes** (Sin nada)

6. Subir nuestro repositorio local al remoto

    `git remote add origin https://github.com/adolfodelarosades/angular-heroes.git`

    `git push -u origin master`

7. Asociar un Tag a la versión inicial y subirla al Remoto

    `git tag -a v0.0.0 -m "Version inicial"`

    `git push --tags`

## Creando la estructura de nuestro proyecto (Componentes navbar y home)

* En la carpeta **app** vamos a crear la carpeta **components** y dentro otra carpeta llamada **shared**

* Vamos a crear nuestro componente **navbar**, nuestra barra de navegación.

    `ng g c components/shared/navbar`

    ```
    CREATE src/app/components/shared/navbar/navbar.component.html (25 bytes)
    CREATE src/app/components/shared/navbar/navbar.component.spec.ts (628 bytes)
    CREATE src/app/components/shared/navbar/navbar.component.ts (269 bytes)
    CREATE src/app/components/shared/navbar/navbar.component.css (0 bytes)
    UPDATE src/app/app.module.ts (414 bytes)
    ```

    Nos crea 4 archivos, pero realmente no vamos a usar ni el **spec.ts** ni el **.css**, los eliminamos.

    En el archivo **.ts** hace la referencia al archivo **.css**

    `styleUrls: ['./navbar.component.css']`

    que eliminamos porque ya no tenemos ese archivo.

* Vamos a crear nuestro componente **home**, nuestra página home.

    `ng g c components/shared/home`

    Eliminamos **spec.ts** y **.css**, en el archivo **.ts** eliminamos la referencia al archivo **.css**

    Y es aquí cuando me doy cuenta que **home** no debería estar en la carpeta **shared**, debería estar en la carpeta **components** ¿Cómo arreglo esto?.

    Podemos arrastrar la carpeta **home** de **shared** a **components**

    Después de hacer lo anterior y cargar la página me muestra el error:

    `Cannot GET /`

    Si veo la consola de la terminal me marca el error:

    `ERROR in src/app/app.module.ts(6,31): error TS2307: Cannot find module './ components/shared/home/home.component'. `

    Voy a **app.module.ts** y veo el fallo:

    `import { HomeComponent } from './components/shared/home/home.component';`

    ya no se encuentra en esa ubicación, elimino **/shared** 

    `import { HomeComponent } from './components/home/home.component';`

    Todo bien ahora, esto lo tendremos que hacer si movemos un componente de una carpeta a otra, pero si lo eliminamos debemos eliminar la referencia al componente en **app.module.ts**.

    Al cargar nuevamente la página ya no marca ningún error.

## Instalando el Bootstrap

Vamos a instalar Bootstrap de 3 formas diferentes, esto será aplicable a cualquier otra librería.

1. Usar BootstrapCDN.

    * Ir a **getbootstrap.com**

    * Ir a Download

    * Buscar BootstrapCDN

    * Incluir las cuatro líneas en nuestro archivo **index.html** de la siguiente forma:

        ```
        <!doctype html>
        <html lang="en">
            <head>
                <meta charset="utf-8">
                <title>Heroes</title>
                <base href="/">

                <meta name="viewport" content="width=device-width, initial-scale=1">
                <link rel="icon" type="image/x-icon" href="favicon.ico">
                <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
            </head>
            <body>
                <app-root></app-root>  
                <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
                <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script>
                <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
            </body>
        </html>
        ```

2. Descargando las librerías Bootstrap en nuestro proyecto local.

    * Ir a **getbootstrap.com**

    * Ir a Download

    * Presionar el botón **Download** para descargar la librería **bootstrap-4.3.1.zip**

    * Descomprimir el archivo **.zip**

    * Copiamos la carpeta **dist**

    * En la carpeta **assets** de nuestro proyecto creamos la carpeta **libs** y allí pegamos la carpeta **dist**

    * Renombramos **dist** por **bootstrap**

    * En el archivo **index.html** en lugar de hacer referencia al CDM haremos referencia a la librería descargada localmente, lo haremos solo para el archivo **.css** pero se podría hacer también para los **.js**, tendríamos que descargarnos **jquery** y **popper**. Nuestro archivo **index.html** queda así:

        ```
        <!doctype html>
        <html lang="en">
            <head>
                <meta charset="utf-8">
                <title>Heroes</title>
                <base href="/">

                <meta name="viewport" content="width=device-width, initial-scale=1">
                <link rel="icon" type="image/x-icon" href="favicon.ico">
                <link rel="stylesheet" href="assets/libs/bootstrap/css/bootstrap.min.css">
            </head>
            <body>
                <app-root></app-root>    
            </body>
        </html>
        ```

3. Instalando Bootstrap usando **npm**

    * Eliminamos las librerías copiadas dentro de **assets**

    * Eliminamos de **index.html** la línea:

        `<link rel="stylesheet" href="assets/libs/bootstrap/css/bootstrap.min.css">`

        Para que quede la versión original del archivo.

    * Ir a **getbootstrap.com**

    * Ir a Download

    * Bajar hasta **npm** y copiamos la línea:

        `npm install bootstrap`

    * En el **Git Bash** estando en la carpeta **heroes** ejecutamos el comando que copiamos añadiéndole **--save** para indicar que es una librería que mi proyecto necesita

        `npm install bootstrap --save`

        ```
        npm WARN bootstrap@4.3.1 requires a peer of jquery@1.9.1 - 3 but none is installed. You must install peer dependencies yourself.
        npm WARN bootstrap@4.3.1 requires a peer of popper.js@^1.14.7 but none is installed. You must install peer dependencies yourself.
        npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.9 (node_modules\fsevents):
        npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.9: wanted {"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"x64"})

        + bootstrap@4.3.1
        added 1 package from 2 contributors and audited 19006 packages in 34.388s
        found 0 vulnerabilities

        ```

    * Al ejecutar este comando descarga **Bootstrap** y lo incluye en los módulos de node **node_modules**, pero también me dice que debo instalar **jquery** y **popper** ya que tiene dependencias con ellos.

        `npm install jquery --save`

        `npm install popper.js --save`

    * Una vez instaladas las librerías y descargadas en **node_modules** hay que indicarle a Angular que las tiene que utilizar, esto se hace en el archivo **angular.json**, este archivo es un archivo de configuración que describe como arranca la aplicación, que favicon va a usar, donde se encuentran los **assets**, cual es la página de estilos general, entre muchas cosas más.  

    * En **angular.json** vamos a modificar los **styles** para indicar que use la librería de **Bootstrap**

        ```
        "styles": [
              "src/styles.css",
              "node_modules/bootstrap/dist/css/bootstrap.min.css"
            ]
        ```
    * Para que entren en acción los cambios necesitamos dar de baja y volverlo a arrancar el servidor, una vez hecho esto vemos que ya toma los estilos css de **Bootstrap** sin necesidad de meter nada en nuestro archivo **index.html**, esta instalado de manera general.
    
     * En **angular.json** vamos a modificar los **scripts** para indicar que use la librería **js** de **Jquery**, **Pooper** y **Bootstrap**, la que tiene más dependencias generalmente va al final.

        ```
        "scripts": [
              "node_modules/jquery/dist/jquery.slim.min.js",
              "node_modules/popper.js/dist/umd/popper.min.js",
              "node_modules/bootstrap/dist/js/bootstrap.min.js"
            ]
        ```

        Intalar así las librerías tiene la desventaja que todas estas librerías son parte del proyecto y hacen que pese un poco más, pero la ventaja que se pueden usar globalmente.

    * Damos nuevamente de baja el servidor y lo volvemos a cargar para que tome los cambios.

## Configurando el navbar

   * De los recursos descargados copiamos todas las imágenes en **assets/img**

   * De los recursos descargados copiamos el **favicon** y lo reemplazamos por el existente en nuestro proyecto. Si recargamos la página se puede ver el nuevo favicon.

   * **NOTA** Cuando tenemos las herramientas de desarrollar abiertas, podemos dar clic derecho en el simbolo de recarga y nos saldrán las siguientes opciones:

        * Volver a cargar normalmente
        * Volver a cargar de forma forzada
        * Vaciar la caché y volver a cargar de forma forzada

        Estas opciones sirven para forzar la recarga.

   * Vamos a implementar nuestro componente **navabar.component.html**, vamos a copiar de la documentación Bootstrap la primer **navbar** que aparece en la documentación.

   * Para meter un logo en nuestra barra, la documentación de Bootstrap nos ayuda:

        ```
        <!-- Just an image -->
        <nav class="navbar navbar-light bg-light">
            <a class="navbar-brand" href="#">
                <img src="/docs/4.3/assets/brand/bootstrap-solid.svg" width="30" height="30" alt="">
            </a>
        </nav>
        ``` 

   * Nuestro **navabar.component.html** queda así:

        ```
        <nav class="navbar navbar-expand-lg navbar-light bg-light">
            <a class="navbar-brand" href="#">
                <img src="assets/img/A-64.png" width="30" height="30" alt="">
            </a>
            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>

            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav mr-auto">
                    <li class="nav-item active">
                        <a class="nav-link" href="#">Home</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#">Link</a>
                    </li>
                </ul>
                <form class="form-inline my-2 my-lg-0">
                    <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
                    <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
                </form>
            </div>
        </nav>
        ```

   * Aun no vemos nada en nuestra página vamos a **app.component.html** y ponemos:

        ```
        <app-navbar></app-navbar>  
        ```

   * Para que la barra de navegación salga oscura se pone:

        `navbar-dark bg-dark`

   * Si cargamos la página ya podemos apreciar nuestra barra de navegación

## Configurando la home

   * En la documentación de **Bootstrap** buscamos **Jumbotron** copiamos el **Fluid jumbotron** y lo copiamos en **home.component.html**, lo personalizamos:

        ```
        <div class="jumbotron jumbotron-fluid">
            <div class="container">
                <h1 class="display-4">Comic App</h1>
                <p class="lead">Esta es una aplicación de comics.</p>
            </div>
        </div>
        ```

   * No podremos ver aun la página hasta que implementemos las rutas.

## Creación componentes about y heroes

   * Vamos a crear los componentes **about** y **heroes** sin **css** ni **test**
    
        ```
        ng g c components/about -is --skipTests
        
        CREATE src/app/components/about/about.component.html (24 bytes)
        CREATE src/app/components/about/about.component.ts (239 bytes)
        UPDATE src/app/app.module.ts (588 bytes)

        ng g c components/heroes -is --skipTests
        CREATE src/app/components/heroes/heroes.component.html (25 bytes)
        CREATE src/app/components/heroes/heroes.component.ts (242 bytes)
        UPDATE src/app/app.module.ts (681 bytes)
        ```

## Rutas en Angular

## RouterLink y RouterLinkActive - Completando las rutas

## Componente Heroes - diseño

## Introducción a los Servicios

## Creando nuestro primer servicio - HeroesService

## Página de Heroes - Diseño con *ngFor

## Rutas con parametros - Router

## Recibiendo parámetros por URL – ActivatedRoute

## Tarea práctica #1 - Componente del héroe

## Resolución de la tarea práctica 1 - Componente del héroe

## Pipes: Transformación visual de la data.

## Buscador de Héroes

## Tarea práctica 2: Crear la pantalla de búsqueda de héroes.

## Resolución de la tarea 2 - Buscador de Héroes

## Plus: Mostrando un mensaje cuando no hay resultados.

## @Input - Recibir información de un componente padre a un hijo

## @Output - Emitir un evento del hijo hacia el padre

## Arreglar detalles de la búsqueda

## Código fuente de la sección
