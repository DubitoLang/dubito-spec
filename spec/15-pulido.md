---
title: "Pulido"
order: 15
mark: pulido
mark_group: plat
---
*Plataforma · optimizador*

# Pulido

**Rol:** optimizador · **En la TCB:** no, si cada pasada se valida

Pulido es el optimizador de la plataforma. Mejora el código generado sin cambiar su significado, y ninguna de sus pasadas necesita confianza si Plomada la valida.

## <a id="optimizacion"></a>Caminos de optimización

<a id="optimizacion-1"></a>Una implementación PUEDE optimizar por cualquiera de dos caminos, o combinarlos: `optimizacion-1`

| Camino                         | Dónde                                                 | Cómo se confía en el resultado                                                                                                                                                                                                                                                   |
|--------------------------------|-------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <a id="optimizacion-2"></a>Sobre Stela `optimizacion-2`   | Transformaciones de Stela a Stela, antes del backend. | El resultado lleva su evidencia y el verificador lo comprueba por completo, igual que el original. La pasada queda fuera de la TCB.                                                                                                                                              |
| <a id="optimizacion-3"></a>En el backend `optimizacion-3` | Pasadas sobre la IR de bajo nivel.                    | Una pasada con validación de traducción produce un testigo que Plomada, el validador de traducción, comprueba; la pasada queda fuera de la TCB y solo Plomada pertenece a ella. Una pasada PUEDE no tener validación: entonces pertenece a la TCB y DEBE figurar en el inventario de confianza de cada binario que la usa (R9). |

<a id="optimizacion-4"></a>Ninguna optimización, por ningún camino, puede alterar: `optimizacion-4`

- <a id="optimizacion-5"></a>el comportamiento observable definido por la semántica de Stela, incluidos el modelo de memoria y el aborto; `optimizacion-5`
- <a id="optimizacion-6"></a>los efectos que el programa ejerce y su orden respecto de los demás efectos; `optimizacion-6`
- <a id="optimizacion-7"></a>la disciplina de tiempo constante: no introduce bifurcaciones, accesos dependientes ni operaciones de latencia variable sobre datos secretos; `optimizacion-7`
- <a id="optimizacion-8"></a>las protecciones de especulación ni los borrados de secretos; `optimizacion-8`
- <a id="optimizacion-9"></a>los puntos de telemetría declarados, que no se eliminan ni se reordenan respecto de los efectos que observan; `optimizacion-9`
- <a id="optimizacion-10"></a>la reproducibilidad: las mismas fuentes, la misma cadena, el mismo destino y el mismo perfil producen los mismos bytes. `optimizacion-10`

### <a id="perfiles-opt"></a>Perfiles de optimización

<a id="optimizacion-11"></a>Un perfil de optimización se define por su objetivo, no por una lista de pasadas: **ninguno** (correspondencia directa con el código fuente, para depuración), **velocidad** o **tamaño**. Qué pasadas usa cada perfil es una decisión de cada implementación. El perfil no cambia el significado, así que no aparece en el diff de significado; queda registrado en la atestación del binario. Con cualquier perfil, la información de depuración sigue siendo correcta para el código que se generó. `optimizacion-11`

## <a id="optimizacion-pendiente"></a>Lo que queda por definir *(Informativa)*

Por implementación, las pasadas de cada perfil de optimización (`anx-implementacion-5`). Todo está registrado en el [anexo A](33-anexo-a.md).

---

← [Speculum](14-speculum.md) · [Índice](README.md) · [Cincel](16-cincel.md) →
