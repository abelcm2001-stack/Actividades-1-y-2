# Actividades 1 y 2

Este trabajo analiza cómo se carga y se ejecuta JavaScript en una página web, y cómo influyen la posición y los atributos de las etiquetas `<script>`.

## Actividad 1: herramientas de desarrollo

Se estudia el funcionamiento de una página real, utilizando YouTube como ejemplo y las herramientas de desarrollo del navegador:

- En **Network** se observa la respuesta HTML recibida por el navegador y se analiza el renderizado inicial de la página mediante SSR (*Server Side Rendering*).
- En **Performance** se graba la actividad de la página para comprobar cómo JavaScript procesa las interacciones y utiliza el hilo principal.
- En la **Consola** se comprueba el funcionamiento del Sandbox del navegador. Al intentar leer directamente un archivo del equipo con `FileReader`, el navegador bloquea la operación porque la página no puede acceder libremente a los archivos del usuario.
- También se analiza el posible bloqueo producido por un script de más de 1 MB. En la carga revisada de YouTube no se encontró ningún archivo individual de ese tamaño; el más grande observado fue de 24,3 kB.

## Actividad 2: formas de cargar scripts

Se crean cinco páginas HTML para comparar distintos métodos de carga de los mismos tres scripts. Cada script realiza muchas iteraciones, escribe mensajes en la consola y cambia el texto del elemento con `id="titulo"`.

- **Escenario A:** los scripts tradicionales están en el `<head>`. Se ejecutan antes de que el `<body>` haya creado el título, por lo que `document.getElementById("titulo")` devuelve `null` y se produce un error.
- **Escenario B:** los scripts se colocan al final del `<body>`, cuando el elemento ya existe, y pueden modificarlo correctamente.
- **Escenario C:** se utiliza el atributo `async`. Los scripts se descargan y ejecutan de forma independiente en cuanto están disponibles, por lo que su orden de ejecución no está garantizado.
- **Escenario D:** se utiliza `defer`. Los scripts se descargan mientras se analiza el HTML, pero esperan hasta que el documento haya sido procesado y mantienen el orden en el que aparecen.
- **Escenario E:** los scripts se cargan como módulos con `type="module"`. Los módulos se ejecutan de forma diferida y tienen un ámbito propio.

## Conclusión

La posición y los atributos de `<script>` cambian el momento en que se ejecuta JavaScript y el acceso que tiene al contenido HTML. Los scripts tradicionales pueden bloquear el análisis de la página, mientras que `async`, `defer` y los módulos permiten controlar mejor la carga. La elección depende de si se necesita respetar el orden de los scripts y de si el contenido HTML debe estar disponible antes de ejecutarlos.