---
title: "Destinos"
order: 20
---
*Plataforma*

# Destinos

Un destino combina una arquitectura, un sistema operativo (o ninguno) y una especificación que define sus intrínsecos. El mismo módulo puede compilarse para cualquier destino cuya especificación provea lo que el módulo requiere.

## <a id="dst-perfiles"></a>Perfiles

|                                                   | core                                     | freestanding                              | hosted                                |
|---------------------------------------------------|------------------------------------------|-------------------------------------------|---------------------------------------|
| Bajo el programa `dst-perfiles-1`                 | Nada: el módulo no puede ejecutarse solo | Hardware                                  | Sistema operativo                     |
| Intrínsecos `dst-perfiles-2`                      | Ninguno                                  | Operaciones de hardware                   | Interfaz del sistema                  |
| Memoria dinámica, tareas y reloj `dst-perfiles-3` | Como requisitos abiertos                 | Con proveedores del programa              | Provistos por la biblioteca estándar  |
| Archivos, red, procesos `dst-perfiles-4`          | No                                       | No                                        | Sí                                    |
| Produce `dst-perfiles-5`                          | Bibliotecas portables                    | Kernels, cargadores de arranque, firmware | Aplicaciones, servicios, herramientas |

<a id="dst-perfiles-6"></a>Una biblioteca se atesta con sus requisitos abiertos y se enlaza en cualquier binario que los provea. El cierre de los requisitos solo se exige al enlazar un binario. `dst-perfiles-6`

## <a id="dst-disp"></a>Disponibilidad

<a id="dst-disp-1"></a>Lo que un programa puede usar depende del destino, pero nunca se descubre en ejecución. Cada módulo tiene requisitos (efectos y extensiones) y cada binario tiene provisiones: los intrínsecos y extensiones garantizadas del destino, los proveedores del paquete raíz y las extensiones detectadas al arrancar, accesibles solo con un testigo. Un binario se enlaza solo si sus requisitos están contenidos en sus provisiones. `dst-disp-1`

### <a id="dst-proveedores"></a>Proveedores

<a id="dst-disp-2"></a>La memoria dinámica, las tareas, el reloj monótono y la telemetría son servicios construidos sobre intrínsecos. La plataforma define sus traits con contratos, y el paquete raíz de un binario elige quién los implementa; una biblioteca nunca provee, solo requiere. En hosted, la biblioteca estándar ofrece proveedores predeterminados sustituibles; en freestanding, los provee el programa. `dst-disp-2`

- <a id="dst-disp-3"></a>**Memoria dinámica.** Cada bloque entregado tiene al menos el tamaño y la alineación pedidos, es disjunto de todo bloque vivo y solo puede liberarse una vez; si no hay memoria, nada cambia. `dst-disp-3`
- <a id="dst-disp-4"></a>**Tareas.** Toda tarea se ejecuta como máximo una vez y termina, se cancela o aborta su región, nunca después de cerrarse su ámbito. Crear una tarea sucede antes que su inicio y su fin sucede antes que la espera por ella. La cancelación solo se observa en operaciones de espera. `dst-disp-4`
- <a id="dst-disp-5"></a>**Reloj monótono.** Nunca retrocede. `dst-disp-5`
- <a id="dst-disp-6"></a>**Telemetría.** Emitir es total y no devuelve nada observable: un proveedor no puede fallar hacia el programa; si no puede entregar una señal, la descarta y lo cuenta. `dst-disp-6`

<a id="dst-disp-7"></a>Un proveedor que no cumple estos contratos no se acepta. Sus propios efectos entran en los requisitos del binario. `dst-disp-7`

### <a id="dst-variantes"></a>Variantes por destino

- <a id="dst-disp-8"></a>Cuando un módulo necesita implementaciones distintas según el destino, cada una es un archivo condicionado. La selección es por archivo, nunca dentro de una función. `dst-disp-8`
- <a id="dst-disp-9"></a>Las condiciones se refieren a perfil, sistema, frontera, base, arquitectura y extensiones, y las variantes de un módulo son mutuamente excluyentes. `dst-disp-9`
- <a id="dst-disp-10"></a>Todas las variantes exportan la misma interfaz, así que quien llama verifica una sola vez para todos los destinos. Un módulo sin variante para un destino no existe en él. `dst-disp-10`

### <a id="dst-capacidades"></a>Extensiones del procesador

<a id="dst-disp-11"></a>Una extensión se usa mediante un testigo de capacidad, que solo se obtiene de forma estática, si el destino la garantiza, o por detección al arrancar, si el destino la declara opcional. Cada operación de una extensión exige su testigo, así que ninguna instrucción de una extensión se ejecuta en una máquina que no la tiene. La versión acelerada y la portable de una función declaran los mismos contratos. `dst-disp-11`

### <a id="dst-lenguajes"></a>Disponibilidad de los lenguajes

<a id="dst-disp-12"></a>Los seis lenguajes existen en los tres perfiles (R11). En cada perfil, un lenguaje ofrece lo que el destino puede sostener; lo que no está disponible en un perfil se rechaza al compilar, nunca falla en ejecución. `dst-disp-12`

| Lenguaje                | core (bibliotecas portables)                                                                                                                                                                               | freestanding (kernel y firmware)                                                                                                                       | hosted (espacio de usuario)                                                                          |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| Zea `dst-disp-13`       | Todo el lenguaje sin memoria dinámica; concurrencia como requisito abierto.                                                                                                                                | Acceso al hardware e interrupciones; memoria dinámica, tareas y reloj con proveedores del programa.                                                    | Todo, con los proveedores y la E/S de la biblioteca estándar.                                        |
| Talud `dst-disp-14`     | Clases, herencia, contratos y despacho sobre objetos por valor o prestados.                                                                                                                                | Además, objetos en memoria dinámica y conteo de referencias con un proveedor; modelado de dispositivos y controladores.                                | Todo, con los proveedores predeterminados.                                                           |
| Solsticio `dst-disp-15` | Funciones sobre datos de tamaño fijo, recursión con medida y manejadores.                                                                                                                                  | Además, clausuras que escapan, tipos recursivos, colecciones y pereza con un proveedor de memoria; efectos de hardware a través de manejadores.        | Todo, con paralelismo sobre las tareas predeterminadas.                                              |
| Voluta `dst-disp-16`    | Macros completas, que se expanden al compilar; funciones sobre escalares, registros y uniones de claves.                                                                                                   | Además, colecciones, texto, datos de forma desconocida y funciones que escapan con un proveedor de memoria.                                            | Todo.                                                                                                |
| Amate `dst-disp-17`     | Relaciones de capacidad declarada en almacenamiento estático o provisto por quien llama; exceder la capacidad es un error declarado. Las reglas sobre hechos constantes se evalúan al compilar.            | Lo mismo que en core y, con un proveedor de memoria, relaciones sin capacidad declarada.                                                               | Todo, con evaluación paralela sobre tareas.                                                          |
| Relevo `dst-disp-18`    | Un conjunto estático de actores con almacenamiento estático y buzones de capacidad fija; la planificación queda como requisito abierto. Sin aborto por región, la supervisión maneja errores como valores. | Además, interrupciones como fuente de mensajes, planificación cooperativa propia y, con proveedores, creación dinámica de actores y aborto por región. | Todo: actores dinámicos repartidos en tareas, aborto por región, plazos con reloj y actores remotos. |

## <a id="dst-concurrencia"></a>Concurrencia por perfil

<a id="dst-concurrencia-1"></a>La transferibilidad, la compartibilidad y los préstamos valen en todos los perfiles. Los atómicos existen hasta el ancho del destino. En freestanding, un manejador de interrupción se trata como una tarea más: lo que comparte es compartible y el estado mutable pasa por atómicos o por secciones críticas, que se implementan enmascarando interrupciones. Las tareas existen en core como requisito abierto, en freestanding con un proveedor y en hosted siempre. `dst-concurrencia-1`

## <a id="dst-componentes"></a>Componentes

<a id="dst-componentes-1"></a>La especificación de cada destino es [Rumbo](19-rumbo.md), y el código del destino lo genera [Cincel](16-cincel.md). `dst-componentes-1`

---

← [Rumbo](19-rumbo.md) · [Índice](README.md) · [Chinampa](21-chinampa.md) →
