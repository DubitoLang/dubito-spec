<!-- SPDX-FileCopyrightText: 2026 Xhunik Nikol Miguel Mutzutz y colaboradores de Dubito -->
<!-- SPDX-License-Identifier: CC-BY-SA-4.0 -->

*Cadena de herramientas*

# dubito

**Rol:** frontends y coordinación · **En la TCB:** no

dubito es la cadena de herramientas de la familia. Traduce el código fuente a la representación intermedia, genera las condiciones de verificación, busca sus pruebas y coordina la mutación, el verificador y el backend.

## <a id="fases"></a>Fases

1.  <a id="fases-1"></a>Análisis del código fuente. `fases-1`
2.  <a id="fases-2"></a>Resolución de nombres e imports por identidad de contenido. `fases-2`
3.  <a id="fases-3"></a>Evaluación en compilación. `fases-3`
4.  <a id="fases-4"></a>Comprobación de tipos, ownership y préstamos, efectos y procedencia. `fases-4`
5.  <a id="fases-5"></a>Reducción a la representación intermedia, con toda abstracción explícita. `fases-5`
6.  <a id="fases-6"></a>Generación de condiciones de verificación (VC) a partir de contratos e instrucciones. `fases-6`
7.  <a id="fases-7"></a>Búsqueda de pruebas con un solucionador dentro del presupuesto; cada prueba encontrada se guarda como certificado comprobable paso a paso. `fases-7`
8.  <a id="fases-8"></a>Mutación de las definiciones nuevas o modificadas. `fases-8`
9.  <a id="fases-9"></a>Verificación y, si se emite la atestación, bajada, optimización y generación de código ([Niveles de representación](#niveles)). `fases-9`

<a id="fases-10"></a>Como dubito no está en la TCB, un error en cualquiera de estas fases produce, como mucho, un módulo que el verificador rechaza. `fases-10`

## <a id="niveles"></a>Niveles de representación

<a id="niveles-1"></a>Un programa pasa por cuatro niveles. Solo el código fuente y el binario existen fuera de la compilación (R3). `niveles-1`

| Nivel                                 | Contenido                                                                                                                            | Garantía                                                                         |
|---------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| Código fuente `niveles-2`             | Texto de uno de los lenguajes de la familia, en forma canónica.                                                                      | Ninguna por sí mismo.                                                            |
| Stela `niveles-3`                     | Representación intermedia con tipos, ownership, efectos, procedencia, contratos y evidencia.                                         | Verificada por el verificador; de ella se deriva la identidad del módulo (R7).   |
| Sillar (IR de bajo nivel) `niveles-4` | Código de tres direcciones en forma de asignación única estática (SSA), con los tipos de máquina y el modelo de memoria del destino. | Correcta por construcción del núcleo del backend o por validación de traducción. |
| Código del destino `niveles-5`        | Instrucciones, datos y metadatos del binario.                                                                                        | La de Cincel, el backend, que pertenece a la TCB.                                |

- <a id="niveles-6"></a>La IR de bajo nivel conserva como anotaciones explícitas todo lo que una optimización DEBE respetar: los datos secretos, las protecciones de especulación, los borrados de secretos, los puntos de telemetría y los límites de los efectos. `niveles-6`
- <a id="niveles-7"></a>Su contenido concreto se define en la etapa siguiente, sin contradecir estos requisitos. `niveles-7`

## <a id="optimizacion"></a>Optimización (Pulido)

<a id="optimizacion-1"></a>Pulido es el optimizador de la plataforma. Una implementación PUEDE optimizar por cualquiera de dos caminos, o combinarlos: `optimizacion-1`

| Camino                         | Dónde                                                 | Cómo se confía en el resultado                                                                                                                                                                                                                                                   |
|--------------------------------|-------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Sobre Stela `optimizacion-2`   | Transformaciones de Stela a Stela, antes del backend. | El resultado lleva su evidencia y el verificador lo comprueba por completo, igual que el original. La pasada queda fuera de la TCB.                                                                                                                                              |
| En el backend `optimizacion-3` | Pasadas sobre la IR de bajo nivel.                    | Cada pasada DEBE tener validación de traducción: produce un testigo que Plomada, el validador de traducción, comprueba, y solo Plomada pertenece a la TCB. Una pasada sin validación pertenece a la TCB y aparece en el inventario de confianza de cada binario que la usa (R9). |

<a id="optimizacion-4"></a>Ninguna optimización, por ningún camino, puede alterar: `optimizacion-4`

- <a id="optimizacion-5"></a>el comportamiento observable definido por la semántica de Stela, incluidos el modelo de memoria y el aborto; `optimizacion-5`
- <a id="optimizacion-6"></a>los efectos que el programa ejerce y su orden respecto de los demás efectos; `optimizacion-6`
- <a id="optimizacion-7"></a>la disciplina de tiempo constante: no introduce bifurcaciones, accesos dependientes ni operaciones de latencia variable sobre datos secretos; `optimizacion-7`
- <a id="optimizacion-8"></a>las protecciones de especulación ni los borrados de secretos; `optimizacion-8`
- <a id="optimizacion-9"></a>los puntos de telemetría declarados, que no se eliminan ni se reordenan respecto de los efectos que observan; `optimizacion-9`
- <a id="optimizacion-10"></a>la reproducibilidad: las mismas fuentes, la misma cadena, el mismo destino y el mismo perfil producen los mismos bytes. `optimizacion-10`

### <a id="perfiles-opt"></a>Perfiles de optimización

<a id="optimizacion-11"></a>Un perfil de optimización se define por su objetivo, no por una lista de pasadas: **ninguno** (correspondencia directa con el código fuente, para depuración), **velocidad** o **tamaño**. Qué pasadas usa cada perfil es una decisión de cada implementación. El perfil no cambia el significado, así que no aparece en el diff de significado; queda registrado en la atestación del binario. Con cualquier perfil, la información de depuración sigue siendo correcta para el código que se generó. `optimizacion-11`

## <a id="directivas"></a>Directivas de compilación

<a id="directivas-1"></a>Una directiva es una anotación dirigida a la cadena de herramientas sobre un paquete, un módulo o una declaración. Su sintaxis sigue los [principios de sintaxis](01-familia.md#fam-sintaxis) y es la misma en los seis lenguajes. Hay dos clases: `directivas-1`

| Clase                     | Ejemplos                                                                                                               | Reglas                                                                                                                                                                |
|---------------------------|------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Sugerencia `directivas-2` | Perfil de optimización de una función, expansión en línea, desenrollado de un bucle, rama probable.                    | NO DEBE cambiar el significado ni debilitar ninguna de las propiedades que la optimización preserva. La cadena PUEDE ignorarla. No aparece en el diff de significado. |
| Exigencia `directivas-3`  | Tiempo constante, sin memoria dinámica, pila acotada, capacidad del procesador requerida, llamada de cola garantizada. | Se verifica: si no se cumple, el módulo se rechaza. Forma parte de la interfaz y aparece en el diff de significado.                                                   |

- <a id="directivas-4"></a>**Sin duplicar el núcleo.** Lo que el núcleo ya expresa como efecto, etiqueta de procedencia o contrato se exige con ese mecanismo; una directiva de exigencia nunca crea una garantía paralela (R4). `directivas-4`
- <a id="directivas-5"></a>**Ámbito.** Una directiva sobre un paquete alcanza a sus módulos, y una sobre un módulo, a sus declaraciones. Entre sugerencias gana la más específica; las exigencias se acumulan y una declaración no puede relajar una exigencia heredada. `directivas-5`
- <a id="directivas-6"></a>**Directivas desconocidas.** Una sugerencia desconocida se ignora con un aviso; una exigencia desconocida es un error. `directivas-6`

## <a id="bootstrap"></a>Construcción de la propia cadena

- <a id="bootstrap-1"></a>La primera implementación puede escribirse en cualquier lenguaje; su elección no forma parte de la especificación ni de la TCB. `bootstrap-1`
- <a id="bootstrap-2"></a>Toda versión DEBE poder reconstruirse desde una base mínima publicada junto con ella. `bootstrap-2`
- <a id="bootstrap-3"></a>Toda compilación es reproducible en el sentido de Reproducible Builds: las mismas fuentes, la misma cadena y el mismo destino producen los mismos bytes. `bootstrap-3`
- <a id="bootstrap-4"></a>Toda versión se valida con doble compilación diversa (Wheeler, 2009): construida por dos cadenas independientes, los binarios DEBEN coincidir bit a bit. `bootstrap-4`

## <a id="review"></a>Diff de significado (Glosa)

<a id="review-1"></a>La forma principal de revisión es Glosa, el diff de significado, que compara dos versiones de la representación intermedia y reporta solo cambios de significado: efectos, contratos, procedencia, errores, comprobaciones en ejecución, telemetría, inventario de confianza y mutantes sobrevivientes. Todo lo que amplía lo que el programa puede hacer o debilita lo que afirma se marca. Los cambios se agrupan en código, demostraciones y pruebas. `review-1`

## <a id="diagnosticos"></a>Diagnósticos y editores

- <a id="diagnosticos-1"></a>Los diagnósticos se emiten en SARIF 2.1.0 (OASIS). `diagnosticos-1`
- <a id="diagnosticos-2"></a>La integración con editores usa el Language Server Protocol. `diagnosticos-2`

## <a id="depuracion"></a>Depuración

- <a id="depuracion-1"></a>La información de depuración se emite en DWARF 5, relaciona el código generado con el código fuente y queda fuera de la identidad del módulo: mover código o comentarios no cambia la identidad. `depuracion-1`
- <a id="depuracion-2"></a>No hay compilación de depuración con otra semántica: la información de depuración nunca cambia el código generado ni las comprobaciones en ejecución. `depuracion-2`
- <a id="depuracion-3"></a>Los datos secretos se muestran redactados por defecto. En lugar del código fantasma, que no existe en ejecución, se muestran los contratos y la clase de evidencia de cada VC. `depuracion-3`
- <a id="depuracion-4"></a>Los proveedores de tareas exponen tareas, ámbitos, regiones, árboles de supervisión y ocupación de buzones. `depuracion-4`
- <a id="depuracion-5"></a>Un informe de aborto puede convertirse en una prueba que reproduce el fallo; un fallo concurrente se reproduce con el motor simulado y su semilla. `depuracion-5`

---

← [Relevo](08-relevo.md) · [Índice](README.md) · [Stela](10-stela.md) →
