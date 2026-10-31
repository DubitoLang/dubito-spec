<!-- SPDX-FileCopyrightText: 2026 Xhunik Nikol Miguel Mutzutz y colaboradores de Dubito -->
<!-- SPDX-License-Identifier: CC-BY-SA-4.0 -->

*Introducción*

# Familia de lenguajes

Seis lenguajes independientes y del mismo rango, cada uno con un paradigma propio. Todos emiten la misma representación intermedia, así que un mismo proyecto puede usarlos juntos.

| Lenguaje                     | Paradigma                        | Dominio típico                                  | Perfiles |
|------------------------------|----------------------------------|-------------------------------------------------|----------|
| [Zea](03-zea.md)             | Sistemas; imperativo y funcional | Núcleos, bibliotecas, kernels, servicios        | Los tres |
| [Talud](04-talud.md)         | Orientado a objetos              | Modelado de dominios con jerarquías estables    | Los tres |
| [Solsticio](05-solsticio.md) | Funcional puro                   | Cálculo, transformación de datos, compiladores  | Los tres |
| [Voluta](06-voluta.md)       | Simbólico, tipado estático       | Lenguajes de dominio, configuración, prototipos | Los tres |
| [Amate](07-amate.md)         | Lógico                           | Reglas de negocio, cumplimiento, permisos       | Los tres |
| [Relevo](08-relevo.md)       | Actores                          | Servicios concurrentes de larga duración        | Los tres |

## <a id="fam-definicion"></a>Definición común

<a id="fam-definicion-1"></a>Las reglas que comparten los seis lenguajes están en el [Núcleo común](02-nucleo.md), que no pertenece a ningún lenguaje. Cada página de lenguaje define solo lo que su paradigma añade. `fam-definicion-1`

## <a id="fam-sintaxis"></a>Principios de sintaxis

<a id="fam-sintaxis-1"></a>La sintaxis concreta de cada lenguaje no se define en esta fase. Cualquier sintaxis que se defina DEBE cumplir: `fam-sintaxis-1`

- <a id="fam-sintaxis-2"></a>Todas las palabras del lenguaje (palabras reservadas, nombres de la biblioteca, valores predefinidos) están en inglés. `fam-sintaxis-2`
- <a id="fam-sintaxis-3"></a>Palabras completas en todo punto donde un revisor toma decisiones: efectos, contratos, propagación de errores, mutabilidad y conversiones de procedencia. `fam-sintaxis-3`
- <a id="fam-sintaxis-4"></a>Los argumentos de una llamada se nombran, salvo en los casos que el lenguaje justifique de forma uniforme. `fam-sintaxis-4`
- <a id="fam-sintaxis-5"></a>Gramática libre de contexto, analizable con anticipación acotada. `fam-sintaxis-5`
- <a id="fam-sintaxis-6"></a>Una única forma canónica para cada programa, aplicada por el formateador sin opciones. `fam-sintaxis-6`
- <a id="fam-sintaxis-7"></a>Ningún comentario puede ocultar código: no hay comentarios de bloque. `fam-sintaxis-7`
- <a id="fam-sintaxis-8"></a>Texto fuente en UTF-8 (RFC 3629) normalizado a NFC (UAX \#15), con identificadores según UAX \#31. `fam-sintaxis-8`

## <a id="fam-objetivos"></a>Objetivos de sintaxis

<a id="fam-objetivos-1"></a>Cada lenguaje tiene un lector y una tarea para los que se optimiza su sintaxis concreta, y un estilo estructural que corresponde a su paradigma. El estilo describe la forma del texto, no sus caracteres; la sintaxis abstracta de cada lenguaje está en su sección de construcciones. `fam-objetivos-1`

| Lenguaje                                       | Lector y tarea                                                                                                      | Estilo estructural                                                                                                                            |
|------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| [Zea](03-zea.md) `fam-objetivos-2`             | Quien revisa código de bajo nivel y necesita ver en cada línea la memoria, los préstamos, los efectos y los costos. | Bloques delimitados de instrucciones y expresiones con precedencia fija. Toda copia, reserva de memoria y conversión tiene una marca visible. |
| [Talud](04-talud.md) `fam-objetivos-3`         | Quien modela un dominio y lee jerarquías, invariantes de clase y redefiniciones.                                    | Declaraciones de clase con sus miembros agrupados, la invariante junto a la clase y la redefinición siempre marcada.                          |
| [Solsticio](05-solsticio.md) `fam-objetivos-4` | Quien razona por ecuaciones sobre transformaciones de datos.                                                        | Definiciones por ecuaciones y casos, aplicación y composición ligeras, y encadenamiento de transformaciones de izquierda a derecha.           |
| [Voluta](06-voluta.md) `fam-objetivos-5`       | Quien escribe código que se manipula como datos: macros y lenguajes de dominio.                                     | Expresiones anidadas uniformes, cuya estructura textual es la del árbol de sintaxis.                                                          |
| [Amate](07-amate.md) `fam-objetivos-6`         | Quien lee reglas de negocio, de cumplimiento o de permisos, a menudo sin ser programador.                           | Cláusulas con cabeza y cuerpo, hechos que se leen como filas de una tabla y consultas separadas de las reglas.                                |
| [Relevo](08-relevo.md) `fam-objetivos-7`       | Quien sigue flujos de mensajes, esperas y supervisión entre actores.                                                | Declaraciones de actor con sus mensajes y manejadores, supervisión declarativa, y envíos y esperas siempre visibles.                          |

### <a id="fam-criterios"></a>Criterios de evaluación

<a id="fam-objetivos-8"></a>Toda propuesta de sintaxis concreta DEBE cumplir los principios de arriba y estos criterios comprobables: `fam-objetivos-8`

- <a id="fam-objetivos-9"></a>**Determinismo.** La gramática se analiza de forma determinista con anticipación acotada; un generador de analizadores la acepta sin conflictos. `fam-objetivos-9`
- <a id="fam-objetivos-10"></a>**Ida y vuelta.** Imprimir un árbol de sintaxis con el formateador y volver a analizarlo produce el mismo árbol. `fam-objetivos-10`
- <a id="fam-objetivos-11"></a>**Localidad.** Un cambio local de significado produce un cambio textual local en la forma canónica. `fam-objetivos-11`
- <a id="fam-objetivos-12"></a>**Visibilidad.** Cada elemento del diff de significado (efectos, contratos, conversiones de procedencia, propagación de errores, mutabilidad y directivas de exigencia) tiene una marca visible en el punto donde ocurre. `fam-objetivos-12`
- <a id="fam-objetivos-13"></a>**Recuperación.** La gramática permite recuperarse de un error de análisis y localizar el diagnóstico en el punto del error. `fam-objetivos-13`
- <a id="fam-objetivos-14"></a>**Coherencia.** Los conceptos comunes (efectos, contratos, procedencia, directivas) usan las mismas palabras en los seis lenguajes. `fam-objetivos-14`

### <a id="fam-eleccion"></a>Elección de la sintaxis

<a id="fam-objetivos-15"></a>La sintaxis concreta de cada lenguaje se elige en la etapa siguiente mediante una propuesta pública que incluye la gramática completa, el formateador de referencia y la traducción de un corpus de ejemplos común a los seis lenguajes. La propuesta se evalúa contra los criterios de arriba y se aprueba con el [proceso de gobierno](24-proyecto.md#pro-gobierno). La sintaxis aprobada es la primera edición del lenguaje. `fam-objetivos-15`

## <a id="fam-admision"></a>Criterio de admisión

<a id="fam-admision-1"></a>Un lenguaje pertenece a la familia si cumple las cinco condiciones: `fam-admision-1`

1.  <a id="fam-admision-2"></a>Emite representación intermedia que el verificador acepta. `fam-admision-2`
2.  <a id="fam-admision-3"></a>No tiene ninguna construcción que suspenda garantías. `fam-admision-3`
3.  <a id="fam-admision-4"></a>Toda característica implícita de su paradigma (despacho virtual, macros, manejo de efectos, planificación de actores) queda explícita en la representación intermedia y visible en el diff de significado. `fam-admision-4`
4.  <a id="fam-admision-5"></a>Define su forma canónica y la aplica el formateador. `fam-admision-5`
5.  <a id="fam-admision-6"></a>Está disponible en los tres perfiles, con sus capacidades adecuadas a cada uno (R11, [Disponibilidad de los lenguajes](13-destinos.md#dst-lenguajes)). `fam-admision-6`

## <a id="fam-interop"></a>Interoperabilidad

<a id="fam-interop-1"></a>Los módulos de distintos lenguajes se importan entre sí como cualquier módulo. Los tipos se corresponden a través de la representación intermedia, así que no hay capa de traducción. La correspondencia está en [Interoperabilidad](21-interop.md#int-familia). `fam-interop-1`

## <a id="fam-limites"></a>Lo que la familia no hace

- <a id="fam-limites-1"></a>**Ejecutar código generado en ejecución.** Ningún lenguaje evalúa código en ejecución ni compila en ejecución: todo lo que se ejecuta pasó por el verificador. `fam-limites-1`
- <a id="fam-limites-2"></a>**Portar lenguajes existentes.** Los seis son lenguajes nuevos diseñados para la plataforma. `fam-limites-2`

---

← [Visión general](00-inicio.md) · [Índice](README.md) · [Núcleo común](02-nucleo.md) →
