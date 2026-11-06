***Parcial 3 Sistemas Operativos***
Integrantes 
Mariana Montoya Deza
Isabel Parra Sierra 
Sofia Rojo Salazar

Descripción 
Compresor y descompresor de archivos desarrollado en C para Linux, utilizando el algoritmo de Huffman de manera concurrente. El proyecto extiende el editor de texto realizado en el Parcial 1, integrando la compresión y descompresión como tareas en segundo plano para que el usuario pueda seguir interactuando con el editor mientras se procesa el archivo. Para esto, se utilizan hilos POSIX y mecanismos de sincronización que permiten procesar los archivos por bloques y mostrar el progreso de la operación.

Funcionalidades
Compresión de archivos mediante el algoritmo de Huffman
Descompresión de archivos
Procesamiento de archivos divididos en bloques
Uso de varios hilos trabajadores
Conteo de frecuencias y codificación concurrente
Escritura de los bloques en el orden correspondiente
Ejecución de la compresión y descompresión en segundo plano
Visualización del progreso de las operaciones
Sincronización del acceso a los archivos
Cancelación de tareas en ejecución
Detección de archivos dañados o incompletos
Pruebas automatizadas
Comandos 
El editor incorpora las siguientes órdenes para trabajar con la compresión y descompresión:

z [destino] — Comprimir el archivo abierto
u <origen.huf> [destino] — Descomprimir un archivo
t — Consultar el estado y progreso de la tarea
c — Cancelar la tarea en ejecución
Pruebas 
El proyecto incluye pruebas automatizadas para verificar la compresión y descompresión de archivos, la integridad de los resultados, el funcionamiento de los hilos, la sincronización y el manejo de errores. Las pruebas se ejecutan mediante los scripts PRUEBAS.sh y PRUEBAS_PARCIAL2.sh, y utilizan pty_driver.c para simular la interacción con el editor. Según los resultados documentados, se obtuvieron 43 de 43 pruebas exitosas para el Parcial 2 y se mantuvieron las 11 pruebas del Parcial 1.

Ejecución 
El proyecto se compila desde la carpeta principal utilizando: bash make Para ejecutar el editor: bash ./editor/text_editor archivo.txt
Una vez abierto el editor, se puede presionar : para ingresar al modo de órdenes y utilizar los comandos de compresión y descompresión disponibles.
Las pruebas se ejecutan mediante:
bash PRUEBAS.sh
bash PRUEBAS_PARCIAL2.sh

Uso de Inteligencia Artificial Este proyecto utilizó herramientas de Inteligencia Artificial como apoyo durante el proceso de desarrollo. Se emplearon principalmente para:
Repasar conceptos relacionados con concurrencia y sincronización
Revisar el código base proporcionado por el profesor
Apoyar la implementación y depuración del programa
Construir y revisar pruebas automatizadas


Apoyar la redacción de la documentación
Consideraciones:

La implementación y el desarrollo del proyecto fueron realizados por los integrantes.
Se revisó y probó el código utilizado durante el desarrollo.
La IA se utilizó como herramienta de apoyo y no co
