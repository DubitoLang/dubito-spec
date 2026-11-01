---
title: "Stela"
order: 10
mark: stela
mark_group: plat
---
*Plataforma · representación intermedia*

# Stela

**Rol:** representación intermedia · **Se ejecuta:** nunca

Stela es la representación intermedia de la plataforma: tipada, con control estructurado, específica de un destino y portadora de su propia evidencia. Los seis lenguajes compilan a ella, el verificador la verifica y el backend la traduce a código nativo.

**Definición normativa**

<a id="stela-1"></a>La semántica de Stela es operacional y DEBE mecanizarse en un asistente de pruebas; ante cualquier diferencia con esta descripción, prevalece la mecanización. `stela-1`

## <a id="stx-garantia"></a>Propiedad garantizada

<a id="stx-garantia-1"></a>Si el verificador acepta un módulo para un destino, toda ejecución de su código sobre una máquina que cumple la especificación de ese destino cumple, hasta terminar o abortar por una comprobación en ejecución declarada: `stx-garantia-1`

- <a id="stx-garantia-2"></a>Ningún desbordamiento aritmético, división por cero, acceso fuera de límites ni lectura de memoria no inicializada. `stx-garantia-2`
- <a id="stx-garantia-3"></a>Ningún uso de un valor movido o liberado, ningún préstamo que sobreviva a su dueño y ningún préstamo exclusivo con otro simultáneo. `stx-garantia-3`
- <a id="stx-garantia-4"></a>Ninguna carrera de datos. `stx-garantia-4`
- <a id="stx-garantia-5"></a>Ningún efecto fuera de los declarados por la función que lo produce. `stx-garantia-5`
- <a id="stx-garantia-6"></a>Ningún flujo entre etiquetas de procedencia que no pase por una justificación, y ningún dato secreto que determine una rama, un índice, una latencia o una salida observable. `stx-garantia-6`
- <a id="stx-garantia-7"></a>Toda postcondición se cumple al retornar. `stx-garantia-7`

<a id="stx-garantia-8"></a>Este enunciado es el teorema principal de la mecanización, junto con la corrección del verificador respecto a la semántica. `stx-garantia-8`

## <a id="stx-principios"></a>Propiedades

- <a id="stx-principios-1"></a>**Control estructurado.** Bloques, bucles e inspecciones anidados; sin saltos arbitrarios. El grafo de control es reducible y cada bucle tiene lugar para su invariante. `stx-principios-1`
- <a id="stx-principios-2"></a>**Forma de asignación única tipada.** Cada valor se define una vez y tiene tipo completo, incluida su etiqueta. `stx-principios-2`
- <a id="stx-principios-3"></a>**Monomórfica.** Sin genéricos ni variables de efecto. `stx-principios-3`
- <a id="stx-principios-4"></a>**Ownership explícito.** Mover, prestar y destruir son operaciones explícitas. `stx-principios-4`
- <a id="stx-principios-5"></a>**Efectos por referencia.** Toda interacción externa es una invocación a un intrínseco del destino, identificado por su identidad, o una llamada a una función con efectos declarados. `stx-principios-5`
- <a id="stx-principios-6"></a>**Afirmaciones de primera clase.** Contratos, citas de lemas, invariantes, VC y evidencia forman parte de la representación. `stx-principios-6`
- <a id="stx-principios-7"></a>**Canónica.** Una sola representación por programa; la identidad de cada definición se deriva de ella, de modo que cada definición es la raíz de un árbol de identidades. `stx-principios-7`
- <a id="stx-principios-8"></a>**Evolución aditiva.** Una versión nueva solo puede añadir construcciones; nunca cambia el significado de una existente. Un módulo válido en una versión lo es en todas las posteriores. `stx-principios-8`

## <a id="stx-modulo"></a>Contenido de un módulo

- <a id="stx-modulo-1"></a>Identidad del módulo, del destino y de cada dependencia; condición de variante; requisitos abiertos (efectos y capacidades usados sin proveer). `stx-modulo-1`
- <a id="stx-modulo-2"></a>Tipos, efectos, etiquetas y sus refinamientos, proveedores, declaraciones nativas y fronteras. `stx-modulo-2`
- <a id="stx-modulo-3"></a>Funciones con su firma, contratos con sus citas y cuerpo. `stx-modulo-3`
- <a id="stx-modulo-4"></a>Conversiones de procedencia y la justificación que autoriza cada una. `stx-modulo-4`
- <a id="stx-modulo-5"></a>Exportaciones y telemetría declarada. `stx-modulo-5`
- <a id="stx-modulo-6"></a>La parte fantasma: funciones fantasma, lemas con sus pasos, extensiones y actualizaciones fantasma. `stx-modulo-6`
- <a id="stx-modulo-7"></a>La evidencia: el presupuesto con que se produjo y la resolución de cada VC. `stx-modulo-7`

<a id="stx-modulo-8"></a>Un módulo es de código (de archivos ejecutables y de demostración) o de pruebas. El código, la parte fantasma, la evidencia y las pruebas tienen identidades separadas, y la del binario depende solo del código. `stx-modulo-8`

## <a id="stx-instr"></a>Operaciones

<a id="stx-instr-1"></a>Control estructurado; llamadas directas, indirectas, de cola y a intrínsecos; aritmética con modo comprobado, modular o explícitamente opcional; comparaciones; conversiones explícitas; constantes y regiones declaradas por el destino; registros, sumas, arreglos y vistas con su VC de límites o de variante; mover, prestar y destruir; lectura, escritura, reserva y liberación de memoria; atómicos y barreras con orden explícito; conversión de etiqueta, solo dentro de una justificación; selección sin bifurcación, barrera de especulación y borrado no eliminable; afirmación y suposición, esta última solo en especificaciones de destino. `stx-instr-1`

## <a id="stx-memoria"></a>Modelo de memoria

<a id="stx-memoria-1"></a>Como la ausencia de carreras de datos se demuestra por tipos, los accesos no atómicos se comportan como en una ejecución secuencial. Los atómicos siguen el modelo formal RC11 (Lahav, Vafeiadis, Kang, Hur y Dreyer, 2017). Los enunciados `stx-memoria-2` a `stx-memoria-5` lo resumen y, ante cualquier diferencia, prevalece RC11; `stx-memoria-6` es una restricción propia de Dubito que se añade al modelo. `stx-memoria-1`

- <a id="stx-memoria-2"></a>Órdenes: relajado, de adquisición (lecturas), de liberación (escrituras), de adquisición y liberación, y secuencialmente consistente. `stx-memoria-2`
- <a id="stx-memoria-3"></a>Una escritura de liberación leída por una lectura de adquisición establece una relación *sucede antes* entre todo lo anterior a la escritura y todo lo posterior a la lectura. `stx-memoria-3`
- <a id="stx-memoria-4"></a>Las operaciones secuencialmente consistentes forman un orden total coherente con *sucede antes*. `stx-memoria-4`
- <a id="stx-memoria-5"></a>Cada ubicación atómica tiene un orden de modificación total, y ninguna lectura devuelve un valor que dependa de sí misma. `stx-memoria-5`
- <a id="stx-memoria-6"></a>No se mezclan accesos atómicos de distinto tamaño sobre la misma ubicación. `stx-memoria-6`

## <a id="stx-vc"></a>Contratos y condiciones de verificación

<a id="stx-vc-1"></a>Los contratos son fórmulas sobre los valores de la representación, con acceso al estado de entrada y al resultado; dentro de una fórmula los enteros son matemáticos. Las fórmulas cubren lo que admite la [lógica de contratos](02-nucleo.md#nuc-contratos), la aritmética de flotantes y decimales, los tipos matemáticos y las medidas estructurales. Las VC se entregan al solucionador en SMT-LIB 2.6. Cada operación que lo requiere genera una VC implícita con una identidad propia, y toda VC y todo contrato DEBEN resolverse con evidencia. `stx-vc-1`

## <a id="stx-evidencia"></a>Evidencia

| Clase                                       | Contenido                                                                                                                                                                                             |
|---------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Certificado `stx-evidencia-1`               | Prueba del solucionador en el formato Alethe, que un comprobador revisa paso a paso sin repetir la búsqueda.                                                                                          |
| Refinamiento `stx-evidencia-2`              | Certificado de que una implementación refina el contrato de su trait o del método que redefine.                                                                                                       |
| Idempotencia `stx-evidencia-3`              | Certificado de que aplicar dos veces una operación idempotente equivale a aplicarla una.                                                                                                              |
| Comprobación en ejecución `stx-evidencia-4` | La VC se compila como comprobación que aborta si falla. Solo para VC desconocidas cuyos términos son todos ejecutables, dentro de la política del paquete; siempre visible en el diff de significado. |
| Mutación `stx-evidencia-5`                  | Por postcondición: cada mutante y su estado (eliminado con su contraejemplo, equivalente con su certificado, o sobreviviente). Determinista y repetible.                                              |

<a id="stx-evidencia-6"></a>Una VC refutada no tiene evidencia: el módulo se rechaza. `stx-evidencia-6`

## <a id="stx-teoremas"></a>Teoremas de la plataforma

<a id="stx-teoremas-1"></a>La mecanización de las semánticas de Stela y de Sillar, junto con la semántica de la arquitectura y el modelo de fugas de cada destino ([Contenido de una especificación](19-rumbo.md#dst-spec)), DEBE demostrar estos teoremas en un asistente de pruebas. T6 y T7 se demuestran para cada destino. Sus enunciados son normativos; su forma exacta se fija con la mecanización. `stx-teoremas-1`

| Teorema                                             | Enunciado                                                                                                                                                          |
|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| T1. Seguridad de tipos `stx-teoremas-2`             | Un módulo bien tipado nunca llega a un estado sin significado (progreso y preservación).                                                                           |
| T2. Seguridad de memoria `stx-teoremas-3`           | Ownership y préstamos excluyen el acceso fuera de límites, el uso tras liberar y las carreras de datos en el modelo de memoria adoptado.                           |
| T3. Corrección de Dintel `stx-teoremas-4`           | Si Dintel acepta un módulo para un destino, toda ejecución cumple sus contratos y no ejerce efectos no declarados, suponiendo la especificación de ese destino.    |
| T4. Corrección de los certificados `stx-teoremas-5` | Si Dintel acepta el certificado de una VC, la VC es válida.                                                                                                        |
| T5. No interferencia `stx-teoremas-6`               | Los valores secretos no influyen en las salidas observables salvo a través de desclasificaciones justificadas.                                                     |
| T6. Tiempo constante `stx-teoremas-7`               | El código bajo la disciplina de tiempo constante no depende de secretos en su duración, sus accesos a memoria ni sus saltos, según el modelo de fugas mecanizado del destino. |
| T7. Corrección de Cincel `stx-teoremas-8`           | El código del destino, según la semántica mecanizada de su arquitectura, refina la semántica de Stela y preserva T5, T6, las protecciones de especulación, los borrados de secretos y los puntos de telemetría.                                 |
| T8. Corrección de Plomada `stx-teoremas-9`          | Si Plomada valida una pasada de optimización sobre Sillar, su salida refina su entrada (incluidos los efectos y su orden) y preserva las demás propiedades de T7. |
| T9. Determinismo `stx-teoremas-10`                  | El resultado de compilar depende solo de las fuentes, la cadena de herramientas, el destino y el perfil de optimización.                                           |

- <a id="stx-teoremas-11"></a>Mientras un teorema no esté mecanizado, toda atestación lo enumera como supuesto en su inventario de confianza (R9). `stx-teoremas-11`
- <a id="stx-teoremas-12"></a>Cada versión de Dintel, Cincel y Plomada declara la versión de la mecanización con la que se corresponde. `stx-teoremas-12`

## <a id="stx-pendiente"></a>Lo que queda por definir *(Informativa)*

La codificación de Stela y la derivación de la identidad a partir de su forma canónica (`anx-pendiente-2`), el formato de la evidencia de mutación (`anx-pendiente-5`) y el asistente de pruebas con la forma exacta de la semántica y de los teoremas (`anx-pendiente-14`). Todo está registrado en el [anexo A](33-anexo-a.md).

---

← [dubito](09-compilador.md) · [Índice](README.md) · [Sillar](11-sillar.md) →
