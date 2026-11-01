---
title: "Voluta"
order: 6
mark: voluta
mark_group: lang
---
*Lenguaje simbólico*

# Voluta

**Paradigma:** simbólico, funcional · **Tipado:** estático, explícito · **Perfiles:** core, freestanding, hosted

Voluta es el lenguaje simbólico de la familia: el código es una estructura de datos y las macros transforman código antes de compilar.

## <a id="vol-clasificacion"></a>Clasificación

| Eje                                    | Voluta                                                                                   |
|----------------------------------------|------------------------------------------------------------------------------------------|
| <a id="vol-clasificacion-1"></a>Paradigma `vol-clasificacion-1`        | Simbólico y funcional; código como dato                                                  |
| <a id="vol-clasificacion-2"></a>Memoria `vol-clasificacion-2`          | Valores inmutables y colecciones persistentes; celdas atómicas como único estado mutable |
| <a id="vol-clasificacion-3"></a>Evaluación `vol-clasificacion-3`       | Estricta                                                                                 |
| <a id="vol-clasificacion-4"></a>Totalidad `vol-clasificacion-4`        | Total por defecto; no terminación explícita                                              |
| <a id="vol-clasificacion-5"></a>Polimorfismo `vol-clasificacion-5`     | Paramétrico con instanciación explícita; multimétodos sobre tipos suma                   |
| <a id="vol-clasificacion-6"></a>Despacho `vol-clasificacion-6`         | Estático; las funciones son valores                                                      |
| <a id="vol-clasificacion-7"></a>Metaprogramación `vol-clasificacion-7` | Macros higiénicas, solo en compilación                                                   |

## <a id="vol-modelo"></a>Modelo

- <a id="vol-modelo-1"></a>**Dos niveles.** Un lector convierte texto en datos, y un conjunto de formas especiales da significado a ciertas estructuras. `vol-modelo-1`
- <a id="vol-modelo-2"></a>**Tipos propios.** Mapas con claves fijas, esquemas con refinamientos y uniones de claves. Acceder a una clave que el tipo no tiene es un error de compilación. Una colección contiene valores de un solo tipo. `vol-modelo-2`
- <a id="vol-modelo-3"></a>**Datos de forma desconocida.** Leer datos produce un valor de forma desconocida, nunca código; convertirlo a un tipo concreto es explícito y puede fallar, y lo leído sigue siendo *external* hasta pasar por una justificación. `vol-modelo-3`
- <a id="vol-modelo-4"></a>**Estado.** Los valores son inmutables; las colecciones son persistentes y se liberan por conteo de referencias. El único estado mutable es la celda, atómica, con efectos de lectura y escritura. `vol-modelo-4`
- <a id="vol-modelo-5"></a>**Módulos.** Cada módulo declara sus importaciones y lo que exporta, con el tipo de cada símbolo exportado. `vol-modelo-5`
- <a id="vol-modelo-6"></a>**Funciones.** Todo parámetro, enlace y resultado declara su tipo. Una llamada a una función de más de un parámetro nombra sus argumentos. Los multimétodos eligen su cuerpo por la variante de un tipo suma y cubren todas las variantes. `vol-modelo-6`
- <a id="vol-modelo-7"></a>**Iteración** sin crecimiento de pila, con medida de terminación o el efecto de no terminación. `vol-modelo-7`
- <a id="vol-modelo-8"></a>**Sin evaluación en ejecución.** No existe evaluar código en ejecución. `vol-modelo-8`

## <a id="vol-macros"></a>Macros

- <a id="vol-macros-1"></a>Una macro recibe formas y devuelve formas, y se ejecuta solo en compilación. El código expandido se comprueba y verifica como cualquier otro; una expansión mal tipada es un error en el sitio de uso. `vol-macros-1`
- <a id="vol-macros-2"></a>**Higiene por conjuntos de ámbitos** (Flatt, 2016). Cada símbolo lleva el conjunto de ámbitos donde aparece; cada expansión añade un ámbito nuevo a los símbolos que introduce, y una referencia se resuelve con el enlace cuyo conjunto de ámbitos es el mayor subconjunto del suyo. Dos candidatos igual de grandes son un error. Una macro solo introduce un nombre visible en el sitio de uso si lo recibe como argumento. `vol-macros-2`
- <a id="vol-macros-3"></a>Los nombres internos de una expansión se derivan de la identidad de la macro y de la posición de uso, de modo que la forma canónica es estable. `vol-macros-3`

## <a id="vol-pendiente"></a>Lo que queda por definir *(Informativa)*

La sintaxis concreta, incluida la forma textual que acepta el lector (`anx-pendiente-1`), y los nombres de su biblioteca de soporte (`anx-pendiente-7`). Todo está registrado en el [anexo A](33-anexo-a.md).

---

← [Solsticio](05-solsticio.md) · [Índice](README.md) · [Amate](07-amate.md) →
