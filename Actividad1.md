1. Auditoria de red(Network).

Youtube utiliza SSR (Server Side Rendering) para el renderizado de la página
Lo he comprobado en las DevTools, dandole a Network -> Doc y después sale la url de youtube y pulsando en ella después le da a response y te muestra el html completo.


2. Destripando el Motor (Performance).

Durante la grabación, lo que está pasando es que al interactuar con youtube, pues JavaScript está procesando y ejecutando.
Esto se ve yendo a Performance y haciendo la grabación y en la parte del Main hacemos aumento de las líneas y si pinchamos en una de ellas nos muestra la interacción que hemos tenido con youtube en este caso.

3. El Sandbox en acción (Consola).
Al ejecutar una línea de código como esta: 
const r= new FileReader(); r.readAsText("C:/Windows/system.ini"); r.onLoad = function(){ console.log(r.result);} :

 El error que me da al meter este código es este: VM673:2 Uncaught TypeError: Failed to execute 'readAsText' on 'FileReader': parameter 1 is not of type 'Blob'.
  at <anonymous>:2:3
(anonymous)	@	V  M673:2.

Aparece este error porque FileReader intentó leer algo que no era un archivo válido y entonces lo que hace el navegador es bloquearlo.
Esto es importante porque el Sandbox impide que una página web acceda libremente a los archivos del usuario.

- Análisis de Bloqueo. 

Comprobación del script superior a 1 MB:

En la carga analizada de YouTube no he encontrado ningún archivo JavaScript individual superior a 1 MB. El archivo de mayor tamaño que me mostró fue de 24,3 kB.
Si un script de más de 1 MB se ejecutara de forma síncrona y tradicional, podría bloquear el hilo principal del navegador durante su descarga, análisis y ejecución.
El uso de un modelo asíncrono y orientado a eventos permite que el navegador siga respondiendo mientras espera o procesa otras tareas, siendo asi una experiencia de usuario más fluida.