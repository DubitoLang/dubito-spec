---
title: "dubito"
order: 9
---
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
| Sillar (IR de bajo nivel) `niveles-4` | Forma de asignación única estática (SSA) sobre un grafo de control, con argumentos de bloque, los tipos de máquina y el modelo de memoria del destino. | Correcta por construcción del núcleo del backend (T7) y preservada por cada pasada que valida Plomada (T8). |
| Código del destino `niveles-5`        | Instrucciones, datos y metadatos del binario.                                                                                        | La de Cincel, el backend, cuyo núcleo pertenece a la TCB.                        |

<a id="niveles-6"></a>Cada nivel posterior a Stela tiene su página: [Sillar](11-sillar.md) es la IR de bajo nivel, [Pulido](15-pulido.md) la optimiza, [Plomada](13-plomada.md) valida cada pasada y [Cincel](16-cincel.md) genera el código del destino. `niveles-6`

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

- <a id="bootstrap-1"></a>La primera implementación PUEDE escribirse en cualquier lenguaje; su elección no forma parte de la especificación ni de la TCB. `bootstrap-1`
- <a id="bootstrap-2"></a>Toda versión DEBE poder reconstruirse desde una base mínima publicada junto con ella. `bootstrap-2`
- <a id="bootstrap-3"></a>Toda compilación es reproducible en el sentido de Reproducible Builds: las mismas fuentes, la misma cadena, el mismo destino y el mismo perfil de optimización producen los mismos bytes (T9). `bootstrap-3`
- <a id="bootstrap-4"></a>Toda versión se valida con doble compilación diversa (Wheeler, 2009): una cadena independiente compila las fuentes de la cadena y produce un compilador intermedio; ese compilador intermedio vuelve a compilar las mismas fuentes, y el resultado DEBE coincidir bit a bit con el binario oficial de la cadena, que se compiló a sí mismo. Los binarios que producen directamente las dos cadenas no tienen por qué coincidir. `bootstrap-4`

## <a id="diagnosticos"></a>Diagnósticos y editores

- <a id="diagnosticos-1"></a>Los diagnósticos se emiten en SARIF 2.1.0 (OASIS). `diagnosticos-1`
- <a id="diagnosticos-2"></a>La integración con editores usa el Language Server Protocol. `diagnosticos-2`

## <a id="depuracion"></a>Depuración

- <a id="depuracion-1"></a>La información de depuración se emite en DWARF 5, relaciona el código generado con el código fuente y queda fuera de la identidad del módulo: mover código o comentarios no cambia la identidad. `depuracion-1`
- <a id="depuracion-2"></a>No hay compilación de depuración con otra semántica: la información de depuración nunca cambia el código generado ni las comprobaciones en ejecución. `depuracion-2`
- <a id="depuracion-3"></a>Los datos secretos se muestran redactados por defecto. En lugar del código fantasma, que no existe en ejecución, se muestran los contratos y la clase de evidencia de cada VC. `depuracion-3`
- <a id="depuracion-4"></a>Los proveedores de tareas exponen tareas, ámbitos, regiones, árboles de supervisión y ocupación de buzones. `depuracion-4`
- <a id="depuracion-5"></a>Un informe de aborto puede convertirse en una prueba que reproduce el fallo; un fallo concurrente se reproduce con el motor simulado y su semilla. `depuracion-5`

## <a id="dubito-pendiente"></a>Lo que queda por definir *(Informativa)*

Los comandos y opciones de la cadena, las extensiones de archivo y los códigos de diagnóstico (`anx-pendiente-13`); la sintaxis común de las directivas (`anx-pendiente-1`); y, por implementación, el solucionador y los presupuestos (`anx-implementacion-3`, `anx-implementacion-9`). Todo está registrado en el [anexo A](33-anexo-a.md).

---

← [Relevo](08-relevo.md) · [Índice](README.md) · [Stela](10-stela.md) →
