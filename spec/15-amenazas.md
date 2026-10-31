<!-- SPDX-FileCopyrightText: 2026 Xhunik Nikol Miguel Mutzutz y colaboradores de Dubito -->
<!-- SPDX-License-Identifier: CC-BY-SA-4.0 -->

*Plataforma*

# Modelo de amenazas

Contra quién se defiende la plataforma, con qué invariante o componente lo detiene y qué queda fuera de su alcance. Complementa el [modelo de confianza](14-confianza.md): aquel dice en qué se confía; este, de quién se desconfía.

## <a id="ame-activos"></a>Activos protegidos

- <a id="ame-activos-1"></a>**Verdad de las atestaciones.** Si existe una atestación para un módulo, el módulo cumple lo que ella afirma, salvo lo que su inventario de confianza enumera. `ame-activos-1`
- <a id="ame-activos-2"></a>**Confidencialidad de los datos secretos**, incluidos el tiempo de ejecución, los accesos a memoria y la ejecución especulativa. `ame-activos-2`
- <a id="ame-activos-3"></a>**Integridad de lo distribuido:** fuentes, atestaciones y binarios. `ame-activos-3`
- <a id="ame-activos-4"></a>**Límites de capacidad:** un módulo no ejerce efectos que no declara. `ame-activos-4`

## <a id="ame-atacantes"></a>Atacantes

| Atacante                                               | Capacidad                                                                                              | Defensa                                                                                                                                                                                                                                                                                                      |
|--------------------------------------------------------|--------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Autor o generador de código engañoso `ame-atacantes-1` | Escribe código que parece correcto y no lo es, incluido código producido por herramientas automáticas. | Contratos verificados (R1), adecuación por mutación (R5), nada implícito (R6), ninguna construcción que suspenda garantías (R8) y revisión por [Glosa](09-compilador.md#review). Lo que no puede detectarse es un contrato correcto que no expresa la intención: por eso la revisión de contratos es humana. |
| Dependencia maliciosa `ame-atacantes-2`                | Publica un paquete que intenta hacer más de lo que declara o suplantar a otro.                         | Efectos y procedencia en la firma, inventario de confianza, regeneración local en Ceiba con identidad atestada y nombres confundibles según UTS \#39.                                                                                                                                                        |
| Registro o espejo comprometido `ame-atacantes-3`       | Sirve contenido alterado, retiene actualizaciones o reescribe el historial.                            | Direccionamiento por contenido, metadatos firmados según TUF, registro de transparencia (RFC 9162) y regeneración local.                                                                                                                                                                                     |
| Cadena de herramientas comprometida `ame-atacantes-4`  | Inserta código al compilar.                                                                            | dubito está fuera de la TCB; compilación reproducible, doble compilación diversa y una TCB mínima.                                                                                                                                                                                                           |
| Entrada externa en ejecución `ame-atacantes-5`         | Envía datos con forma o contenido hostil.                                                              | Etiqueta de procedencia *external*, conversión solo por justificaciones y fronteras asíncronas con modelo de fallos.                                                                                                                                                                                         |
| Observador de canales laterales `ame-atacantes-6`      | Mide tiempos, accesos a caché o efectos de la ejecución especulativa.                                  | Disciplina de tiempo constante, protecciones de especulación y borrado de secretos, preservados por toda optimización.                                                                                                                                                                                       |
| Par remoto o plugin malicioso `ame-atacantes-7`        | Viola el protocolo de una frontera o intenta salir del techo de un plugin.                             | Modelo de fallos de la frontera, atestación de pares verificados y techo de interfaz, efectos y confianza de cada plugin.                                                                                                                                                                                    |

## <a id="ame-cadena"></a>Cadena de suministro

<a id="ame-cadena-1"></a>Las amenazas a la cadena de suministro se clasifican con el modelo de amenazas de SLSA 1.2, y cada una se asocia a la defensa de la tabla anterior que la cubre. `ame-cadena-1`

## <a id="ame-debilidades"></a>Clases de debilidad excluidas

<a id="ame-debilidades-1"></a>Las clases de debilidad que la plataforma excluye por construcción se identifican con CWE. Cada una tiene pruebas en el conjunto de pruebas de conformidad: `ame-debilidades-1`

| CWE                                  | Debilidad                                            | La excluye                                            |
|--------------------------------------|------------------------------------------------------|-------------------------------------------------------|
| CWE-787, CWE-125 `ame-debilidades-2` | Escritura y lectura fuera de límites                 | Tipos, préstamos y contratos de acceso                |
| CWE-416, CWE-476 `ame-debilidades-3` | Uso después de liberar y referencia nula             | Ownership y ausencia de referencias nulas             |
| CWE-190 `ame-debilidades-4`          | Desbordamiento de enteros                            | Aritmética con comportamiento declarado y VC de rango |
| CWE-362 `ame-debilidades-5`          | Condición de carrera                                 | Transferibilidad, compartibilidad y modelo de memoria |
| CWE-20 `ame-debilidades-6`           | Validación incorrecta de la entrada                  | Procedencia y justificaciones                         |
| CWE-208 `ame-debilidades-7`          | Diferencia de tiempo observable                      | Disciplina de tiempo constante                        |
| CWE-1420 `ame-debilidades-8`         | Exposición por ejecución transitoria                 | Protecciones de especulación                          |
| CWE-14 `ame-debilidades-9`           | Eliminación del borrado de búferes por el compilador | Borrado de secretos que ninguna optimización elimina  |

## <a id="ame-fuera"></a>Fuera de alcance

- <a id="ame-fuera-1"></a>Hardware defectuoso o malicioso más allá de lo que declara su especificación de destino, y los ataques físicos. `ame-fuera-1`
- <a id="ame-fuera-2"></a>Errores en la propia TCB: se reducen con la mecanización de los [teoremas de la plataforma](10-stela.md#stx-teoremas) y se gestionan con la [política de vulnerabilidades](24-proyecto.md#pro-seguridad). `ame-fuera-2`
- <a id="ame-fuera-3"></a>La denegación de servicio por agotamiento de recursos del sistema, salvo lo que acotan los presupuestos, las capacidades y la contrapresión. `ame-fuera-3`
- <a id="ame-fuera-4"></a>La ingeniería social contra mantenedores, que se mitiga con el proceso de gobierno y no con la plataforma. `ame-fuera-4`

---

← [Modelo de confianza](14-confianza.md) · [Índice](README.md) · [Estuco](16-estuco.md) →
