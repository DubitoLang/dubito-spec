---
title: "Modelo de confianza"
order: 26
---
*Plataforma*

# Modelo de confianza

**Principio:** confianza mínima, declarada y enumerada · **Quién elige:** el programador, entre lo que el destino admite · **Predeterminado:** la opción de menor confianza

Ningún programa puede suspender sus garantías, pero todo programa se ejecuta sobre algo que no demuestra: el hardware, el sistema operativo y, a veces, código de terceros. Este modelo define qué puede confiarse, dónde, cómo se reduce al mínimo y cómo queda escrito, igual para cualquier destino.

## <a id="conf-principios"></a>Principios

- <a id="conf-principios-1"></a>**Ninguna suspensión dentro del programa** (R8). `conf-principios-1`
- <a id="conf-principios-2"></a>**Confianza mínima.** Entre las formas de hacer algo que el destino admite, la predeterminada es la que confía en menos. `conf-principios-2`
- <a id="conf-principios-3"></a>**Confianza declarada.** Lo que no se demuestra solo puede venir del destino o de una frontera declarada en el código. `conf-principios-3`
- <a id="conf-principios-4"></a>**Confianza enumerada.** Cada atestación lista exactamente en qué confía, y el diff de significado marca todo aumento (R9). `conf-principios-4`
- <a id="conf-principios-5"></a>**Aislar lo que no puede verificarse.** El código no verificado de terceros nunca comparte memoria con el programa si el destino ofrece una forma de separarlo; si no la ofrece, no se admite. `conf-principios-5`
- <a id="conf-principios-6"></a>**Garantías condicionales explícitas.** Cuando una garantía depende de algo que nadie puede controlar, se enuncia como condición. `conf-principios-6`
- <a id="conf-principios-7"></a>**Elección del programador** entre las opciones que el destino admite; la elección queda en la atestación. `conf-principios-7`

## <a id="conf-capas"></a>Capas de confianza

| Capa                                      | Contenido                                                                                       | Quién la fija                          |
|-------------------------------------------|-------------------------------------------------------------------------------------------------|----------------------------------------|
| Núcleo de la plataforma `conf-capas-1`    | Dintel con su comprobador de pruebas; el núcleo de Cincel (bajada, selección de instrucciones, asignación de registros y enlazado) con Plomada; y las pasadas sin validación que un binario declare | El proyecto; auditado y reconstruible  |
| Base de la mecanización `conf-capas-6`    | El núcleo del asistente de pruebas y las definiciones mecanizadas: las semánticas de Stela, de Sillar y de la arquitectura de cada destino, el modelo de fugas y los enunciados de los teoremas de la plataforma | El proyecto; auditada                  |
| Especificación del destino `conf-capas-2` | Semántica de intrínsecos, arranque, aborto y convención de llamada                              | Mantenedores de cada destino; auditada |
| Plataforma subyacente `conf-capas-3`      | Hardware y la parte del sistema que exige el tipo de frontera                                   | El tipo de frontera                    |
| Fronteras declaradas `conf-capas-4`       | Código nativo aislado, anfitriones de bibliotecas exportadas, plugins, pares externos           | El programador                         |

<a id="conf-capas-5"></a>El núcleo de la plataforma, la base de la mecanización y la especificación del destino forman la TCB. La plataforma subyacente es inevitable. La cuarta es opcional y nunca amplía lo que la TCB garantiza: solo añade valores *external* o condiciones explícitas. `conf-capas-5`

<a id="conf-capas-7"></a>Esta es la única definición de la TCB; las demás páginas remiten a ella. La base de la mecanización no se ejecuta al compilar: se confía en ella porque de ella se derivan las garantías de los teoremas de la plataforma. Mientras un teorema no esté mecanizado, su enunciado figura como supuesto en el inventario de confianza ([Teoremas de la plataforma](10-stela.md#stx-teoremas)). `conf-capas-7`

## <a id="conf-fronteras"></a>Tipos de frontera del sistema

| Tipo                                      | Interfaz estable del sistema                         | Se confía en                                        | Aislamiento posible                  |
|-------------------------------------------|------------------------------------------------------|-----------------------------------------------------|--------------------------------------|
| Ninguna `conf-fronteras-1`                | No hay sistema: el programa corre sobre el hardware  | Hardware y especificación                           | Lo que el programa construya         |
| Llamadas al sistema `conf-fronteras-2`    | Las llamadas del kernel                              | Kernel                                              | Procesos                             |
| Biblioteca del sistema `conf-fronteras-3` | Una biblioteca; las llamadas al sistema son privadas | Kernel y las funciones de la biblioteca que se usan | Procesos                             |
| Capacidades `conf-fronteras-4`            | Las invocaciones de un núcleo basado en capacidades  | Un núcleo mínimo                                    | Dominios de protección               |
| Enlazado `conf-fronteras-5`               | Un sistema compilado dentro del mismo binario        | El sistema completo                                 | Ninguno, salvo protección de memoria |
| Plano `conf-fronteras-6`                  | Interrupciones o tablas sin protección de memoria    | El sistema y todo lo que se cargue                  | Ninguno                              |
| Gestionado `conf-fronteras-7`             | Un entorno de ejecución que impone su propio modelo  | El entorno                                          | El que ofrezca                       |

- <a id="conf-fronteras-8"></a>En un sistema enlazado, el sistema puede escribirse en un lenguaje de la familia y verificarse; si no, la especificación lo declara completo y entra en su TCB. `conf-fronteras-8`
- <a id="conf-fronteras-9"></a>Sin aislamiento posible, un programa no puede importar código nativo; solo la especificación puede incluir componentes nativos, declarados uno por uno. `conf-fronteras-9`
- <a id="conf-fronteras-10"></a>Un sistema puede ofrecer más de una frontera; el programador elige. `conf-fronteras-10`

## <a id="conf-opciones"></a>Opciones elegibles

| Decisión                                                          | Opciones                                                           | Predeterminada                                                      |
|-------------------------------------------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------|
| Base de la biblioteca estándar `conf-opciones-1`                  | Llamadas al sistema o biblioteca del sistema                       | Llamadas al sistema si existen                                      |
| Aislamiento del código nativo `conf-opciones-2`                   | Proceso, dominio o capacidades de hardware                         | El más fuerte que admite el destino                                 |
| Funciones aisladas de la biblioteca del sistema `conf-opciones-3` | En el proceso o en un compartimento                                | Lo que marque el destino; el programa puede aislar más, nunca menos |
| Biblioteca exportada `conf-opciones-4`                            | En el proceso anfitrión o como servicio                            | En el proceso, con la condición declarada                           |
| Relación con un componente externo `conf-opciones-5`              | Exportar, servicio, nativo aislado, base del sistema o par externo | La de menor confianza que el caso admita                            |
| Plugins `conf-opciones-6`                                         | Ninguno, verificados dentro de un techo, o no verificados aislados | Ninguno                                                             |
| Comprobaciones en ejecución `conf-opciones-7`                     | Máximo por paquete y si se admiten en funciones públicas           | Ninguna en funciones públicas                                       |

## <a id="conf-aislamiento"></a>Modos de aislamiento

| Modo                                         | Mecanismo                                                                               |
|----------------------------------------------|-----------------------------------------------------------------------------------------|
| Proceso `conf-aislamiento-1`                 | Espacio de direcciones separado con privilegios reducidos al mínimo autorizado          |
| Dominio `conf-aislamiento-2`                 | Dominio de protección de un núcleo de capacidades, con solo las capacidades autorizadas |
| Capacidades de hardware `conf-aislamiento-3` | Mismo proceso, con punteros de capacidad que limitan lo que el código puede direccionar |

<a id="conf-aislamiento-4"></a>Un mecanismo solo se admite como aislamiento si el código aislado no puede revocarlo ni cambiar sus propios permisos. `conf-aislamiento-4`

## <a id="conf-inventario"></a>Inventario de confianza

<a id="conf-inventario-1"></a>El verificador calcula para cada módulo, y para cada binario al enlazar, un inventario que forma parte de la atestación: el destino y su frontera; la base elegida; cada intrínseco alcanzado, marcando los de la biblioteca del sistema y los aislados; cada biblioteca nativa con su modo de aislamiento y efectos; los cargadores de plugins con su techo; los pares verificados aceptados; las garantías condicionales; las especulaciones no mitigadas; los avisos reconocidos; y el número de comprobaciones en ejecución. El diff de significado marca todo aumento. `conf-inventario-1`

## <a id="conf-exportadas"></a>Bibliotecas exportadas

<a id="conf-exportadas-1"></a>Una biblioteca de la familia cargada en un proceso no verificado no puede protegerse de que ese proceso escriba en su memoria. Su garantía se enuncia así: *si el anfitrión respeta la convención de llamada, no escribe en la memoria de la biblioteca y la llama según sus contratos de concurrencia, todas las garantías de la biblioteca se cumplen.* Sus precondiciones se comprueban en la entrada. Ejecutada como servicio en su propio proceso, a través de una frontera asíncrona, la garantía deja de ser condicional. `conf-exportadas-1`

## <a id="conf-destinos"></a>Adaptar un destino

1.  <a id="conf-destinos-1"></a>Identificar la interfaz que el sistema promete mantener estable y elegir el tipo de frontera. `conf-destinos-1`
2.  <a id="conf-destinos-2"></a>Declarar sus intrínsecos con contratos tan débiles como haga falta para ser verdaderos; lo que el sistema no garantiza llega como *external*. `conf-destinos-2`
3.  <a id="conf-destinos-3"></a>Marcar como aisladas las partes que dependen de configuración o de código cargado en ejecución. `conf-destinos-3`
4.  <a id="conf-destinos-4"></a>Declarar los modos de aislamiento posibles y su mecanismo de reducción de privilegios. `conf-destinos-4`
5.  <a id="conf-destinos-5"></a>Definir aborto, aborto por región si es posible, arranque, convención de llamada, formato ejecutable, fronteras asíncronas y mecanismo de espera. `conf-destinos-5`
6.  <a id="conf-destinos-6"></a>Escribir la biblioteca estándar del destino como variantes con la interfaz común. `conf-destinos-6`

---

← [Interoperabilidad](25-interop.md) · [Índice](README.md) · [Modelo de amenazas](27-amenazas.md) →
