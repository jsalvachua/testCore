# CORE Evaluacion

## Instalación
Copiar el archivo `credentials.sample.json` a `credentials.json` y rellenar con los datos de github.

Ejecutar `npm install`.

## Uso
Ejecutar `node generate_assignments.js [nombre-del-curso]`: Genera todas la prácticas del curso en la carpeta `_deliverables` y las sube a GitHub

Ejecutar `node generate_assignment.js [nombre-del-curso] [nombre-de-la-practica]`: Genera una práctica concreta en la carpeta `_deliverables` y la sube a GitHub

Asignar un valor al parámetro `DEBUG` en el arranque permite generar las prácticas en modo desarrollo (sin subir a GitHub y con la solución inyectada).

## Funcionamiento

Al ejecutar  `node generate_assignment.js [nombre-del-curso] [nombre-de-la-practica]` se genera en el directorio `_deliverables` el código que aparecerá en el repositorio de la práctica y se suben los contenidos a la cuenta de Github configurada, en el repositorio `https://www.github.com/[nombre-de-la-cuenta]/[nombre-del-curso]-[nombre-de-la-practica]`.

Al ejecutar `genera_practicas [nombre-del-curso]` se rellena la estructura `_deliverables` con las prácticas del curso seleccionado y se suben automáticamente cada uno de los repositorios del curso a la cuenta de Github configurada `https://www.github.com/[nombre-de-la-cuenta]/[nombre-del-curso]-[nombre-de-la-practica]`.

### Generación

El entregable final de cada práctica aparecerá en la carpeta `_deliverables` y se compondrá de los archivos que aparecen en las siguientes carpetas (por orden de prioridad):
- Directorio `[nombre-del-curso]/[nombre-de-la-practica]`
- Directorio `[nombre-del-curso]/_common`
- Directorio `_common`

En la estructura ofrecida por defecto cada práctica debe contener al menos (este comportamiento puede ser modificado):
- Un directorio `tests` con un archivo llamado `checks.test.js` que contendrá las pruebas mocha de la práctica
- (Opcional) Una carpeta `_solution` con la solución

En el contenido de todos los archivos copiados, se sustituirá la plantilla de texto `ASSIGNMENT_NAME` por el nombre de la práctica basado en el nombre de la carpeta.

### Prueba de las Prácticas

Si se activa el parámetro `DEBUG`, una vez generados los repositorios en `_deliverables` se copiará sobre ellos el contenido de las carpetas (por orden de prioridad):
- Directorio `[nombre-del-curso]/[nombre-de-la-practica]/_solution`
- Directorio `[nombre-del-curso]/_solution`
- Directorio `_solution`

El directorio resultante NO se subirá a GitHub.

## Estructura

### Directorio "_common"

Archivos comunes para TODAS las prácticas.

#### Directorio "\[nombre_del_curso]"

Directorio correspondiente a un curso con subdirectorios:
- Carpeta `_common`: Archivos comunes para todas las prácticas
- Carpeta `_solution`: Archivos comunes de la solución
- Un directorio por cada práctica del curso.

#### Directorio "\[nombre_del_curso]/_common"

Archivos comunes para todas las prácticas de un curso concreto. 

### Directorio "_historicos"

Versiones del sistema empleadas en años previos.

#### Directorio "_historicos/plantillas"

Plantillas de ejemplo para distintos tipos de test local:
- **Interno**: Wrappea el lanzado de la entrega
    - **librería**: examina el código entregado
    - **std**: interactúa con stdin/stdout/stderr
- **Externo**: corre independientemente de la entrega
    - **socket**: interactúa con un socket
    - **web**: interactúa con un servidor web
