---
title: "Zea"
order: 3
mark: zea
mark_group: lang
---
*Lenguaje de sistemas*

# Zea

**Paradigma:** sistemas · **Perfiles:** core, freestanding, hosted

Zea es el lenguaje de sistemas de la familia: imperativo, con ownership y préstamos, sin soporte en ejecución, y capaz de describir desde un cargador de arranque hasta un servicio de red.

## <a id="zea-clasificacion"></a>Clasificación

| Eje                                    | Zea                                                          |
|----------------------------------------|--------------------------------------------------------------|
| <a id="zea-clasificacion-1"></a>Paradigma `zea-clasificacion-1`        | Imperativo, funcional y genérico; especificación declarativa |
| <a id="zea-clasificacion-2"></a>Nivel `zea-clasificacion-2`            | Sistemas: de freestanding a aplicaciones                     |
| <a id="zea-clasificacion-3"></a>Memoria `zea-clasificacion-3`          | Ownership y préstamos                                        |
| <a id="zea-clasificacion-4"></a>Evaluación `zea-clasificacion-4`       | Estricta, de izquierda a derecha                             |
| <a id="zea-clasificacion-5"></a>Totalidad `zea-clasificacion-5`        | Total por defecto; no terminación solo con su efecto         |
| <a id="zea-clasificacion-6"></a>Polimorfismo `zea-clasificacion-6`     | Paramétrico (monomorfizado) y por traits con contratos       |
| <a id="zea-clasificacion-7"></a>Despacho `zea-clasificacion-7`         | Estático; dinámico solo con objetos de trait                 |
| <a id="zea-clasificacion-8"></a>Herencia `zea-clasificacion-8`         | No; composición y traits                                     |
| <a id="zea-clasificacion-9"></a>Metaprogramación `zea-clasificacion-9` | Solo evaluación en compilación                               |
| <a id="zea-clasificacion-10"></a>Concurrencia `zea-clasificacion-10`    | Concurrencia estructurada; ausencia de carreras por tipos    |

## <a id="zea-construcciones"></a>Construcciones

- <a id="zea-construcciones-1"></a>**Funciones.** Su firma declara parámetros, resultado, efectos, contratos y, si convierte procedencia, la conversión que justifica. Un parámetro se recibe por valor, por préstamo compartido o por préstamo exclusivo. `zea-construcciones-1`
- <a id="zea-construcciones-2"></a>**Métodos e implementaciones.** Un método es una función cuyo primer parámetro es el receptor; las implementaciones de traits siguen las reglas de [Traits](02-nucleo.md#nuc-traits). `zea-construcciones-2`
- <a id="zea-construcciones-3"></a>**Clausuras.** Declaran qué capturan y cómo. Según su captura se invocan muchas veces sin mutar, muchas veces mutando o una sola vez. Sus efectos son parte de su tipo. `zea-construcciones-3`
- <a id="zea-construcciones-4"></a>**Expresiones.** Las condicionales, la inspección de variantes y los bloques son expresiones; la inspección es exhaustiva y admite guardas. La asignación no produce valor. `zea-construcciones-4`
- <a id="zea-construcciones-5"></a>**Bucles.** Declaran invariante y medida de terminación; sin medida exigen el efecto de no terminación. `zea-construcciones-5`
- <a id="zea-construcciones-6"></a>**Operadores.** Tienen significado fijo por tipo; no hay sobrecarga definida por el usuario. `zea-construcciones-6`
- <a id="zea-construcciones-7"></a>**Llamadas de cola.** Pueden marcarse como garantizadas, y el compilador rechaza la marca fuera de posición de cola. `zea-construcciones-7`
- <a id="zea-construcciones-8"></a>**Resultados no usados.** Ignorar un resultado con error es un error de compilación; descartarlo es explícito. `zea-construcciones-8`
- <a id="zea-construcciones-9"></a>**Errores.** La propagación es explícita y no convierte tipos sola: propagar exige que el error sea el de la función, y la variante con envoltura aplica un constructor explícito. Un tipo de error puede acumular los puntos de propagación por los que pasa. `zea-construcciones-9`

## <a id="zea-bajo-nivel"></a>Bajo nivel

<a id="zea-bajo-nivel-1"></a>Zea expresa lo que el software de sistemas necesita del hardware sin suspender garantías: `zea-bajo-nivel-1`

- <a id="zea-bajo-nivel-2"></a>Layout de registros (empaquetado, alineación) y campos de bits. `zea-bajo-nivel-2`
- <a id="zea-bajo-nivel-3"></a>Secciones del enlazador y exportación de funciones con la convención de llamada de la plataforma. `zea-bajo-nivel-3`
- <a id="zea-bajo-nivel-4"></a>Manejadores de interrupción en freestanding, verificados como tareas: lo que comparten es compartible y el estado mutable pasa por atómicos o por secciones críticas. `zea-bajo-nivel-4`
- <a id="zea-bajo-nivel-5"></a>Cota de pila declarada para tareas cuya pila no puede acotarse por análisis. `zea-bajo-nivel-5`
- <a id="zea-bajo-nivel-6"></a>Regiones de memoria y E/S mapeada declaradas por el destino, con acceso a través de sus intrínsecos. `zea-bajo-nivel-6`
- <a id="zea-bajo-nivel-7"></a>Declaración de proveedores (memoria dinámica, tareas, reloj, telemetría), solo en el paquete raíz de un binario. `zea-bajo-nivel-7`

## <a id="zea-concurrencia"></a>Concurrencia y E/S

<a id="zea-concurrencia-1"></a>Zea usa directamente los ámbitos, las tareas y la E/S de la plataforma ([Entrada y salida](23-es.md)) y los atómicos del [modelo de memoria](10-stela.md#stx-memoria), con orden explícito en cada operación. `zea-concurrencia-1`

## <a id="zea-pendiente"></a>Lo que queda por definir *(Informativa)*

La sintaxis concreta (`anx-pendiente-1`), que se elige según la [elección de la sintaxis](01-familia.md#fam-eleccion), y los nombres de su biblioteca de soporte (`anx-pendiente-7`). Todo está registrado en el [anexo A](33-anexo-a.md).

---

← [Núcleo común](02-nucleo.md) · [Índice](README.md) · [Talud](04-talud.md) →
