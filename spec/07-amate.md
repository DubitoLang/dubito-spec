---
title: "Amate"
order: 7
mark: amate
mark_group: lang
---
*Lenguaje lógico*

# Amate

**Paradigma:** lógico · **Perfiles:** core, freestanding, hosted

Amate expresa reglas, no pasos: se declaran relaciones de entrada, hechos y reglas, y el compilador deriva todas sus consecuencias. Cada conclusión puede acompañarse del árbol de reglas y hechos que la produjo.

## <a id="alm-clasificacion"></a>Clasificación

| Eje                              | Amate                                                                                      |
|----------------------------------|--------------------------------------------------------------------------------------------|
| <a id="alm-clasificacion-1"></a>Paradigma `alm-clasificacion-1`  | Lógico: cláusulas de Horn sin símbolos de función, con negación y agregados estratificados |
| <a id="alm-clasificacion-2"></a>Nivel `alm-clasificacion-2`      | Bibliotecas de reglas invocadas desde otros lenguajes                                      |
| <a id="alm-clasificacion-3"></a>Memoria `alm-clasificacion-3`    | Relaciones inmutables                                                                      |
| <a id="alm-clasificacion-4"></a>Evaluación `alm-clasificacion-4` | Punto fijo mínimo por estratos; resultado determinista                                     |
| <a id="alm-clasificacion-5"></a>Efectos `alm-clasificacion-5`    | Ninguno, salvo memoria dinámica y, opcionalmente, tareas                                   |
| <a id="alm-clasificacion-6"></a>Totalidad `alm-clasificacion-6`  | Siempre total                                                                              |

## <a id="alm-modelo"></a>Relaciones y reglas

- <a id="alm-modelo-1"></a>Un módulo declara relaciones de entrada, intermedias y de salida, con columnas tipadas: escalares, enumeraciones importadas o tuplas de ellos. Cada salida se exporta como una función que recibe las relaciones de entrada de las que depende y devuelve la salida como dueño. `alm-modelo-1`
- <a id="alm-modelo-2"></a>Un hecho es una fila constante. Una regla deriva su cabeza para cada asignación de variables que satisface su cuerpo: átomos, átomos negados, comparaciones y asignaciones aritméticas. `alm-modelo-2`
- <a id="alm-modelo-3"></a>Cada variable declara su tipo en su primera aparición en la regla. `alm-modelo-3`
- <a id="alm-modelo-4"></a>**Seguridad.** Toda variable de la cabeza, de un átomo negado o de una comparación aparece en un átomo positivo del cuerpo o se asigna a partir de variables que aparecen en uno. `alm-modelo-4`
- <a id="alm-modelo-5"></a>**Claves.** Una clave declara que unas columnas determinan la fila: precondición sobre las entradas u obligación sobre las relaciones derivadas. `alm-modelo-5`
- <a id="alm-modelo-6"></a>**Estratificación.** Una relación solo puede negarse o agregarse si pertenece a un estrato inferior. `alm-modelo-6`
- <a id="alm-modelo-7"></a>**Agregados.** Suma, conteo, mínimo y máximo agrupan por las demás columnas de la cabeza. `alm-modelo-7`
- <a id="alm-modelo-8"></a>**Terminación.** En una regla recursiva, ningún argumento de la cabeza se calcula con aritmética. El dominio activo es finito y todo programa termina. `alm-modelo-8`
- <a id="alm-modelo-9"></a>**Determinismo.** La semántica es la del modelo perfecto de los programas estratificados (Apt, Blair y Walker, 1988); las salidas se entregan ordenadas. `alm-modelo-9`
- <a id="alm-modelo-10"></a>**Explicaciones.** Una salida puede devolver, con cada fila, una derivación: la regla, las filas usadas y sus propias derivaciones hasta los hechos de entrada, con las negaciones como ausencias comprobadas. Se guarda una sola derivación por fila, la primera en el orden canónico de las reglas. `alm-modelo-10`

## <a id="alm-especificos"></a>Contratos, efectos y pruebas

- <a id="alm-especificos-1"></a>Una precondición restringe una relación de entrada; una postcondición es una propiedad de una salida que el verificador DEBE demostrar; una restricción de integridad se impone a las relaciones intermedias. `alm-especificos-1`
- <a id="alm-especificos-2"></a>Las relaciones fantasma se definen con reglas en los archivos de demostración, y los lemas enuncian propiedades de las relaciones y listan sus pasos: otros lemas o el desarrollo de una regla. `alm-especificos-2`
- <a id="alm-especificos-3"></a>La mutación elimina literales, invierte comparaciones, cambia agregados y quita negaciones, con R5. `alm-especificos-3`
- <a id="alm-especificos-4"></a>La evaluación no puede fallar: es total y sin efectos observables. Las precondiciones de las entradas se verifican en el llamador o se comprueban en la frontera. `alm-especificos-4`
- <a id="alm-especificos-5"></a>Una relación derivada lleva la etiqueta de procedencia más específica común a las relaciones de las que depende; si no existe, el programa se rechaza. La conversión de etiquetas ocurre en el lenguaje que recibe la salida. `alm-especificos-5`
- <a id="alm-especificos-6"></a>Una salida puede evaluarse en paralelo con el efecto de tareas, con resultado idéntico al secuencial. No hay E/S ni telemetría: las explicaciones son el registro de auditoría. `alm-especificos-6`
- <a id="alm-especificos-7"></a>Una prueba declara hechos de entrada y las filas esperadas en una salida. `alm-especificos-7`

## <a id="alm-pendiente"></a>Lo que queda por definir *(Informativa)*

La sintaxis concreta (`anx-pendiente-1`), que se elige según la [elección de la sintaxis](01-familia.md#fam-eleccion), y los nombres de su biblioteca de soporte (`anx-pendiente-7`). Todo está registrado en el [anexo A](33-anexo-a.md).

---

← [Voluta](06-voluta.md) · [Índice](README.md) · [Relevo](08-relevo.md) →
