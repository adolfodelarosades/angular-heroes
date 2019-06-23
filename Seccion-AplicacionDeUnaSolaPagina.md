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

## Configurando el navbar y otros componentes

## Rutas en Angular

## RouterLink y RouterLinkActive - Completando las rutas

## Componente Heroes - diseño

## Introducción a los Servicios

## Creando nuestro primer servicio - HeroesService

## Página de Heroes - Diseño con *ngFor

## Rutas con parametros - Router

## Recibiendo parámetros por URL – ActivatedRoute

## Tarea práctica #1 - Componente del héroe

## Resolución de la tarea práctica #1 - Componente del héroe

## Pipes: Transformación visual de la data.

## Buscador de Héroes

## Tarea práctica #2: Crear la pantalla de búsqueda de héroes.

## Resolución de la tarea 2 - Buscador de Héroes

## Plus: Mostrando un mensaje cuando no hay resultados.

## @Input - Recibir información de un componente padre a un hijo

## @Output - Emitir un evento del hijo hacia el padre

## Arreglar detalles de la búsqueda

## Código fuente de la sección
