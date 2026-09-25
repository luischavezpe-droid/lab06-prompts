# Tarea: Mi prompt profesional 
## Funcionalidad elegida

Diseño e implementación de un módulo de gestión y CRUD (Crear, Leer, Actualizar, Eliminar) de productos para un sistema de inventario, incluyendo persistencia de datos y validaciones de lógica de negocio.

## Version 1: prompt basico 

Hazme un CRUD de productos en Python.

Qué cambió / Estado inicial: Se planteó una solicitud directa y genérica sin especificar la tecnología de almacenamiento, el formato de respuesta, el marco de trabajo ni las reglas del negocio.

Por qué: Es el punto de partida habitual cuando se busca una solución rápida mediante inteligencia artificial.

Resultado / Deficiencia: Genera un script básico con estructuras de datos volátiles en memoria (listas o diccionarios), sin persistencia real, sin validación de datos y sin organización profesional del código.

## Version 2

Crea un script de Python que implemente un CRUD (Crear, Leer, Actualizar, Eliminar) para productos de un inventario. Cada producto debe tener id, nombre, precio y stock. Devuelve el código con comentarios explicando qué hace cada función y añade una pequeña prueba al final.
Qué cambió respecto a la v1: Se definieron explícitamente las propiedades de la entidad (id, nombre, precio, stock), la inclusión de comentarios explicativos y un bloque de pruebas ejecutables.

Por qué: Para acotar el modelo de datos y evitar que la IA asuma campos irrelevantes o estructuras ambiguas.

Qué mejoró en la respuesta: La IA entregó funciones modulares bien documentadas y un ejemplo funcional al final del archivo. Sin embargo, mantuvo la información en memoria, no incluyó validaciones para precios o stock negativos y usó formatos de respuesta desordenados.

## Version 3: prompt final

[Rol]
Actúa como un Desarrollador Backend Senior especializado en Python y arquitectura limpia de software.

[Contexto]
Estamos desarrollando el prototipo de un módulo ligero de gestión de inventario para una tienda minorista local. El sistema se ejecutará en un entorno restringido de servidores antiguos donde no es posible instalar dependencias externas de PyPI ni utilizar entornos virtuales complejos.

[Instrucción]
Diseña e implementa una clase o módulo ejecutable en Python que gestione el CRUD completo (Crear, Leer, Actualizar, Eliminar) de productos. Cada producto debe contener los campos: id (autoincremental), nombre (texto), precio (flotante positivo) y stock (entero no negativo).

[Restricciones]
- Usa únicamente la biblioteca estándar de Python (módulo sqlite3 para la persistencia).
- Queda strictly prohibido el uso de librerías externas o frameworks como SQLAlchemy, FastAPI, Pandas o Django.
- Incluye validaciones explícitas para evitar precios menores o iguales a cero y stock negativo.

[Ejemplos]
Entrada deseada para creación:
crear_producto(nombre="Teclado Mecánico", precio=45.50, stock=10)

Salida esperada (diccionario o tupla):
{"id": 1, "nombre": "Teclado Mecánico", "precio": 45.50, "stock": 10, "estado": "creado"}

[Formato de respuesta]
Estructura tu respuesta estrictamente en tres secciones Markdown:
1. ### Decisiones de Diseño: Explicación de máximo 2 párrafos sobre cómo estructuraste la base de datos sqlite3 y las validaciones.
2. ### Código Fuente: Un único bloque de código Python limpio, modular, con Type Hints y Docstrings.
3. ### Pruebas Ejecutables: Un bloque de código de ejemplo que ejecute ordenadamente las 4 operaciones CRUD e imprima los resultados en consola.
Qué cambió respecto a la v2: Se incorporaron los 5 componentes estructurales de un prompt profesional (Rol, Contexto, Instrucción, Ejemplos y Formato) y se añadió una restricción técnica clave (sin librerías externas, uso exclusivo de sqlite3).

Por qué: Para garantizar un código modular, mantenible y ejecutable de inmediato en entornos con restricciones técnicas sin requerir instalaciones de terceros.

Qué mejoró en la respuesta: Generó una solución completa con persistencia SQLite, validación rigurosa de tipos y rangos, manejo de errores y una entrega dividida exactamente en las tres secciones Markdown solicitadas.

## Componentes del prompt final 

| Componente | Fragmento del prompt final ||
| ----------- | -------------- | ------------------------- |
| Rol           | "Actúa como un Desarrollador Backend Senior especializado en Python y arquitectura limpia de software."         |
| Contexto         | "Estamos desarrollando el prototipo de un módulo ligero de gestión de inventario... El sistema se ejecutará en un entorno restringido de servidores antiguos donde no es posible instalar dependencias externas..."         |
| Instruccion           | "Diseña e implementa una clase o módulo ejecutable en Python que gestione el CRUD completo (Crear, Leer, Actualizar, Eliminar) de productos..."          |
| Ejemplos        | "Entrada deseada: crear_producto(nombre="Teclado Mecánico", precio=45.50, stock=10) | Salida esperada: {"id": 1, "nombre": "Teclado Mecánico", ...}"          |
| Formato        | "Estructura tu respuesta estrictamente en tres secciones Markdown: 1. ### Decisiones de Diseño ... 2. ### Código Fuente ... 3. ### Pruebas Ejecutables"     |

## Evaluacion del resultado

| Criterios de Evaluacion | Cumple (Si/No)  | Observacion |
| ----------- | -------------- | ------------------------- |
| Sin bibliotecas externas    | Si        | El código utiliza únicamente el módulo nativo sqlite3 de la librería estándar de Python. |
| Presencia de los 5 componentes | Si         | Se identifican claramente el Rol, Contexto, Instrucción, Ejemplos y Formato en la estructura.|
| Validacion de negocio implemenadas | Si         | Rechaza la inserción o actualización con precio $precio \le 0$ o $stock < 0$. |
| Cumplimiento del formato de salida   | Si         | La respuesta se organiza en tres bloques Markdown con los encabezados exactos pedidos. |

## Errores que evite

Ser demasiado general:
En la versión 1 solo se pidió "un CRUD". Para evitar respuestas vagas, en la versión 3 se definieron exactamente la tecnología de persistencia (sqlite3), los nombres y tipos de atributos, y la necesidad de validar rangos numéricos.

No indicar el formato de entrega:
Al no especificar la estructura, las IAs suelen intercalar texto explicativo largo con bloques de código fragmentados. Se evitó este problema exigiendo tres secciones Markdown delimitadas (### Decisiones de Diseño, ### Código Fuente y ### Pruebas Ejecutables).
