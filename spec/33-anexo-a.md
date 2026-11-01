---
title: "Anexo A"
order: 33
---
*Referencia · anexo A*

# Definido por el destino, por la implementación o pendiente

Dubito no tiene comportamiento indefinido: todo programa aceptado tiene un único significado. Lo que esta especificación no fija pertenece a una de tres categorías, y cada punto está enumerado aquí, como exige R9: lo decide el destino, lo decide la implementación o queda pendiente de que la especificación lo defina en una etapa siguiente.

## <a id="anx-reglas"></a>Reglas

- <a id="anx-reglas-1"></a>Lo definido por el destino lo DEBE declarar su especificación de destino (Rumbo). `anx-reglas-1`
- <a id="anx-reglas-2"></a>Lo definido por la implementación lo DEBE documentar la declaración de conformidad del producto. `anx-reglas-2`
- <a id="anx-reglas-3"></a>Todo punto que afecta a un binario DEBE quedar registrado en su atestación. `anx-reglas-3`
- <a id="anx-reglas-4"></a>Ningún punto de este anexo puede cambiar el significado de un programa aceptado respecto de la semántica de Stela; solo puede hacer que un programa se acepte o se rechace para un destino. `anx-reglas-4`
- <a id="anx-reglas-5"></a>Lo pendiente lo fija la especificación por propuesta pública según el [proceso de gobierno](30-proyecto.md#pro-gobierno). Mientras no esté fijado, un producto que lo necesite hace una elección provisional según `cnf-requisitos-5`, y esa elección no es una decisión de la implementación que sobreviva a la definición. `anx-reglas-5`
- <a id="anx-reglas-6"></a>Todo lo concreto que esta especificación deja sin fijar figura en una de las tres tablas de este anexo. Un punto concreto que falte aquí es una errata. `anx-reglas-6`

## <a id="anx-destino"></a>Definido por el destino

| Punto                                                                                                                               | Dónde se define en esta especificación                                                             |
|-------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| <a id="anx-destino-1"></a>Perfil, sistema operativo y tipo de frontera del sistema `anx-destino-1`                                                            | [Rumbo](19-rumbo.md)                                                                               |
| <a id="anx-destino-2"></a>Tamaño y alineación de los tipos de máquina; ancho máximo de los atómicos `anx-destino-2`                                           | [Contenido de una especificación](19-rumbo.md#dst-spec); [Concurrencia por perfil](20-destinos.md#dst-concurrencia) |
| <a id="anx-destino-3"></a>Intrínsecos, arranque y forma de reportar el aborto `anx-destino-3`                                                                 | [Rumbo](19-rumbo.md)                                                                               |
| <a id="anx-destino-4"></a>Extensiones del procesador garantizadas y opcionales `anx-destino-4`                                                                | [Destinos](20-destinos.md)                                                                         |
| <a id="anx-destino-5"></a>Convención de llamada externa `anx-destino-5`                                                                                       | [Contenido de una especificación](19-rumbo.md#dst-spec); [Cincel](16-cincel.md#dst-backend)       |
| <a id="anx-destino-6"></a>Modos de aislamiento disponibles y base de std `anx-destino-6`                                                                      | [Modos de aislamiento](26-confianza.md#conf-aislamiento); [Bases de std](21-chinampa.md#std-bases) |
| <a id="anx-destino-7"></a>Semántica formal de la arquitectura y modelo de fugas de canal lateral que cubre la disciplina de tiempo constante `anx-destino-7`  | [Contenido de una especificación](19-rumbo.md#dst-spec); [Procedencia](02-nucleo.md#nuc-procedencia) |
| <a id="anx-destino-8"></a>Orden de bytes de los tipos `anx-destino-8`                                                                                         | [Contenido de una especificación](19-rumbo.md#dst-spec)                                            |
| <a id="anx-destino-9"></a>Cómo se implementa el punto flotante, siempre con la semántica de IEEE 754 `anx-destino-9`                                          | [Contenido de una especificación](19-rumbo.md#dst-spec)                                            |
| <a id="anx-destino-10"></a>Semántica del aborto y si se admite aborto por región `anx-destino-10`                                                              | [Contenido de una especificación](19-rumbo.md#dst-spec); [Aborto](22-errores.md#err-aborto)        |
| <a id="anx-destino-11"></a>Formato ejecutable `anx-destino-11`                                                                                                 | [Contenido de una especificación](19-rumbo.md#dst-spec)                                            |
| <a id="anx-destino-12"></a>Operaciones de latencia independiente de los datos, protecciones de especulación y protección de memoria con secretos `anx-destino-12` | [Contenido de una especificación](19-rumbo.md#dst-spec); [Ejecución especulativa](02-nucleo.md#nuc-secretos-especulacion) |
| <a id="anx-destino-13"></a>Longitud de la ventana especulativa que modela el análisis `anx-destino-13`                                                         | [Ejecución especulativa](02-nucleo.md#nuc-secretos-especulacion)                                   |
| <a id="anx-destino-14"></a>Fronteras asíncronas que provee y su modelo de fallos `anx-destino-14`                                                              | [Contenido de una especificación](19-rumbo.md#dst-spec)                                            |
| <a id="anx-destino-15"></a>Mecanismo de reducción de privilegios `anx-destino-15`                                                                              | [Adaptar un destino](26-confianza.md#conf-destinos); [Cincel](16-cincel.md#dst-backend)            |

## <a id="anx-implementacion"></a>Definido por la implementación

| Punto                                                                                                                                                                            | Dónde se define en esta especificación                   |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------|
| <a id="anx-pendiente-1"></a>Elección provisional de la sintaxis concreta de cada lenguaje, mientras esté pendiente (`anx-pendiente-1`) `anx-implementacion-1`                                                | [Elección de la sintaxis](01-familia.md#fam-eleccion)    |
| <a id="anx-pendiente-2"></a>Elección provisional de la codificación de Stela y de Sillar y de los demás formatos pendientes (`anx-pendiente-2` a `anx-pendiente-17`) `anx-implementacion-2`                 | [Lo que esta versión no define](31-conformidad.md#cnf-requisitos-5) |
| <a id="anx-implementacion-3"></a>Solucionador usado y valor del presupuesto del solucionador `anx-implementacion-3`                                                                                               | [Fases](09-compilador.md#fases)                          |
| <a id="anx-implementacion-4"></a>Selección de mutantes dentro de los operadores adoptados `anx-implementacion-4`                                                                                                  | [Speculum](14-speculum.md)                               |
| <a id="anx-implementacion-5"></a>Pasadas de cada perfil de optimización `anx-implementacion-5`                                                                                                                    | [Perfiles de optimización](15-pulido.md#perfiles-opt)    |
| <a id="anx-implementacion-6"></a>Motores y proveedores predeterminados que ofrece `anx-implementacion-6`                                                                                                          | [Motores](23-es.md#es-motor)                             |
| <a id="anx-implementacion-7"></a>Texto de los diagnósticos `anx-implementacion-7`                                                                                                                                 | [Diagnósticos y editores](09-compilador.md#diagnosticos) |
| <a id="anx-implementacion-8"></a>Límites de traducción: anidamiento, tamaño de módulo y número de declaraciones; cada implementación los documenta y un programa que los excede se rechaza `anx-implementacion-8` | [Límites de traducción](31-conformidad.md#cnf-requisitos-6) |
| <a id="anx-implementacion-9"></a>Presupuesto de pasos de la evaluación en compilación; agotarlo es un error igual en cualquier máquina `anx-implementacion-9`                                                     | [Evaluación en compilación](02-nucleo.md#nuc-comptime)   |

## <a id="anx-pendiente"></a>Pendiente de definir por la especificación

Estos puntos los fijará la especificación en la etapa siguiente ([Fases](30-proyecto.md#pro-fase)), sin contradecir lo que ya está fijado.

| Punto                                                                                                                                        | Dónde se exige                                                                                                                       |
|----------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| <a id="anx-pendiente-1"></a>Sintaxis concreta de cada lenguaje y sintaxis común de las directivas `anx-pendiente-1`                                                      | [Elección de la sintaxis](01-familia.md#fam-eleccion); [Directivas](09-compilador.md#directivas)                                     |
| <a id="anx-pendiente-2"></a>Codificación de Stela y de Sillar, y derivación de la identidad a partir de la forma canónica `anx-pendiente-2`                              | [Propiedades de Stela](10-stela.md#stx-principios); [Sillar](11-sillar.md#sillar-concreto)                                          |
| <a id="anx-pendiente-3"></a>Predicado de evidencia de las atestaciones, y algoritmo de firma y gestión de claves dentro de DSSE `anx-pendiente-3`                        | [Atestación](12-dintel.md#dintel-atestacion)                                                                                         |
| <a id="anx-pendiente-4"></a>Formato del testigo que comprueba Plomada `anx-pendiente-4`                                                                                  | [Plomada](13-plomada.md#plomada-proceso)                                                                                             |
| <a id="anx-pendiente-5"></a>Formato de la evidencia de mutación `anx-pendiente-5`                                                                                        | [Evidencia](10-stela.md#stx-evidencia); [Speculum](14-speculum.md#elk-criterio)                                                     |
| <a id="anx-pendiente-6"></a>Formato y codificación de las especificaciones de destino `anx-pendiente-6`                                                                  | [Contenido de una especificación](19-rumbo.md#dst-spec)                                                                              |
| <a id="anx-pendiente-7"></a>Contenido concreto de la biblioteca estándar: módulos, nombres y firmas `anx-pendiente-7`                                                    | [Lo que el lenguaje requiere](21-chinampa.md#std-requerido)                                                                          |
| <a id="anx-pendiente-8"></a>Combinador del hash derivado y formato de la representación textual derivada `anx-pendiente-8`                                               | [Derivación](02-nucleo.md#nuc-derivacion)                                                                                            |
| <a id="anx-pendiente-9"></a>Formato del inventario de confianza, del manifiesto de telemetría y de los campos propios del informe de aborto `anx-pendiente-9`             | [Inventario de confianza](26-confianza.md#conf-inventario); [Observabilidad](24-observabilidad.md#obs-principios); [Aborto](22-errores.md#err-aborto) |
| <a id="anx-pendiente-10"></a>Formato del manifiesto y del archivo de bloqueo de los paquetes `anx-pendiente-10`                                                           | [Manifiesto y bloqueo](28-ceiba.md#ceiba-manifiesto)                                                                                 |
| <a id="anx-pendiente-11"></a>Protocolo del registro `anx-pendiente-11`                                                                                                    | [Pochteca](29-pochteca.md#pochteca-modelo)                                                                                           |
| <a id="anx-pendiente-12"></a>Formato de la descripción de la interfaz exportada `anx-pendiente-12`                                                                        | [Hacia afuera](25-interop.md#int-export)                                                                                             |
| <a id="anx-pendiente-13"></a>Comandos y opciones de las herramientas, extensiones de archivo y códigos de diagnóstico `anx-pendiente-13`                                  | [Fase del proyecto](00-inicio.md#inicio-fase); [Diagnósticos y editores](09-compilador.md#diagnosticos)                              |
| <a id="anx-pendiente-14"></a>Asistente de pruebas, y forma exacta de las semánticas y de los teoremas mecanizados `anx-pendiente-14`                                      | [Stela](10-stela.md); [Semántica de Sillar](11-sillar.md#sillar-semantica); [Teoremas de la plataforma](10-stela.md#stx-teoremas)   |
| <a id="anx-pendiente-15"></a>Forma en que un paquete declara su edición `anx-pendiente-15`                                                                                | [Compatibilidad](30-proyecto.md#pro-compatibilidad); [Manifiesto y bloqueo](28-ceiba.md#ceiba-manifiesto)                            |
| <a id="anx-pendiente-16"></a>Formato del conjunto de pruebas de conformidad y de su trazabilidad `anx-pendiente-16`                                                       | [Conjunto de pruebas de conformidad](31-conformidad.md#cnf-pruebas)                                                                  |
| <a id="anx-pendiente-17"></a>Formato en que se presenta el diff de significado `anx-pendiente-17`                                                                          | [Glosa](18-glosa.md#review)                                                                                                          |

---

← [Estándares adoptados](32-estandares.md) · [Índice](README.md) · [Fundamentos de diseño](34-fundamentos.md) →
