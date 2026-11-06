***Parcial 3 Sistemas Operativos***

**Integrantes**
Mariana Montoya Deza 
Isabel Parra Sierra
Sofia Rojo Salazar

**Descripción**
El proyecto es una solución desarrollada en C para Linux que busca reforzar la seguridad de los archivos proyectados en memoria mediante mmap(). El proyecto se realiza para la evaluación parcial práctica-teórica de Sistemas Operativos de EAFIT (2026-2), cuyo objetivo es diseñar e implementar mecanismos de seguridad, integridad y control de acceso en la capa del kernel.
La solución implementa un módulo cargable del kernel (LKM) que supervisa operaciones de proyección de archivos y cambios de permisos. También incorpora políticas de seguridad, una política global W^X, auditoría de eventos y una bóveda cifrada accesible mediante /dev/mmvault.

**Funcionalidades**
* Intercepción y supervisión de solicitudes relacionadas con mmap().
* Supervisión de cambios de permisos mediante mprotect().
* Aplicación de reglas de seguridad asociadas a la identidad del archivo.
* Control de permisos de lectura, escritura y ejecución.
* Aplicación de la política W^X.
* Registro de eventos de seguridad y consulta de estadísticas.
* Auditoría mediante /proc/mmguard/policy, /proc/mmguard/stats y /proc/mmguard/log.
* Bóveda cifrada disponible mediante /dev/mmvault.
* Cifrado de páginas con AES-256-CTR.
* Verificación de integridad mediante HMAC-SHA256.
* Descifrado de páginas bajo demanda.
* Pruebas de políticas, semántica, bóveda, W^X y concurrencia.
* Auditoría complementaria mediante eBPF.
* Medición del rendimiento de las operaciones mmap().

**Comandos**
El módulo permite configurar reglas y consultar información de auditoría mediante las interfaces creadas en /proc/mmguard.
* sudo ./scripts/load.sh — Cargar el módulo MMGuard.
* sudo ./scripts/unload.sh — Descargar el módulo.
* cat /proc/mmguard/policy — Consultar las políticas configuradas.
* cat /proc/mmguard/stats — Consultar las estadísticas.
* cat /proc/mmguard/log — Consultar los eventos registrados.
* echo "add /ruta/archivo asx" | sudo tee /proc/mmguard/policy — Agregar una regla para un archivo.
* echo "wx 1" | sudo tee /proc/mmguard/policy — Activar la política global W^X.
* echo "clear" | sudo tee /proc/mmguard/policy — Limpiar las reglas.

**Opciones de las reglas**
* a — Auditar las operaciones del archivo.
* s — Denegar proyecciones compartidas que soliciten escritura.
* p — Denegar proyecciones privadas que soliciten escritura.
* x — Denegar proyecciones que soliciten ejecución.
* d — Denegar el acceso, excepto para el UID autorizado.

**Pruebas**
El proyecto incluye pruebas automatizadas para comprobar las políticas de seguridad, el comportamiento de las operaciones de memoria, la bóveda cifrada, las restricciones W^X y el manejo de condiciones de concurrencia.

**Las pruebas se ejecutan desde la carpeta principal mediante**
sudo ./scripts/run_all_tests.sh

**Resultados documentados**

* Kernel 5.15.0-203-generic: compilación correcta y 90 de 90 verificaciones exitosas.
* Kernel 6.8.0-147-generic: compilación correcta; no se documenta ejecución de las pruebas.
* Kernel 6.17.0-42-generic: compilación correcta y 90 de 90 verificaciones exitosas.

Los registros se encuentran en la carpeta resultados/.

**Ejecución**
El proyecto está diseñado para Linux de 64 bits. Se requieren herramientas de compilación y los encabezados correspondientes al kernel.
Instalar las dependencias principales:
sudo apt update
sudo apt install build-essential linux-headers-$(uname -r)
Compilar el proyecto desde la carpeta principal:
make
También es posible compilar por separado:
make module
make user
Cargar el módulo:
sudo ./scripts/load.sh
Ejecutar las pruebas:
sudo ./scripts/run_all_tests.sh
Ejecutar las mediciones de rendimiento:
sudo ./scripts/run_bench.sh
Ejecutar la auditoría eBPF:
sudo bpftrace ebpf/mmap_audit.bt -c "sh scripts/ebpf_workload.sh"
Descargar el módulo:
sudo ./scripts/unload.sh
Limpiar los archivos generados:
make clean
Estrategia de seguridad implementada

La solución se desarrolla en la capa del kernel para supervisar operaciones que no pueden controlarse completamente mediante bibliotecas o programas en espacio de usuario.
Se utiliza kretprobes sobre los puntos security_mmap_file y security_file_mprotect para evaluar las solicitudes de proyección y modificación de permisos.
Las reglas se asocian con la identidad del archivo mediante su dispositivo y número de inodo. Además, la política W^X busca impedir que una región tenga simultáneamente permisos de escritura y ejecución.

**Uso de Inteligencia Artificial**
Las herramientas de Inteligencia Artificial se pueden utilizar como apoyo durante las fases de exploración, diseño, implementación y verificación del proyecto.
Entre sus posibles usos se encuentran:
* Repasar conceptos de memoria virtual, mmap(), mprotect(), Page Faults y Copy-On-Write.
* Comprender estructuras y mecanismos del kernel relacionados con la seguridad de archivos.
* Explorar alternativas de arquitectura, como módulos LKM, hooks del kernel y eBPF.
* Apoyar la revisión y depuración del código en C.
* Proponer casos de prueba para políticas de acceso, cifrado, integridad y concurrencia.
* Apoyar la organización y redacción de la documentación.

La entrega del parcial también solicita documentar los prompts utilizados, analizar posibles alucinaciones técnicas y explicar el procedimiento de validación manual y compilación contra los headers del kernel.

**Consideraciones**
* MMGuard es una implementación académica y experimental; no debe utilizarse como mecanismo de seguridad de producción.
* La bóveda utiliza claves generadas al cargar el módulo y mantiene su contenido en memoria; no debe considerarse almacenamiento persistente.
* La compatibilidad depende de la versión y configuración del kernel de Linux.
* La carga del módulo requiere permisos de administrador. Secure Boot puede impedir la carga de módulos que no estén firmados.
* La auditoría eBPF complementa los mecanismos del módulo, pero no observa necesariamente cada lectura o escritura después de que una página queda mapeada.
* Se recomienda realizar las pruebas en una máquina virtual.

arlo directamente en el archivo README.md de tu repositorio.
