---
title: "Observabilidad"
order: 24
---
*Plataforma*

# Observabilidad

**Rol:** telemetría declarada y revisable · **En la TCB:** no

Lo que un programa reporta sobre sí mismo forma parte de su interfaz revisable. Toda señal de telemetría se declara con su nombre y sus campos tipados, se emite bajo un efecto, respeta la procedencia y aparece en el diff de significado.

## <a id="obs-principios"></a>Principios

- <a id="obs-principios-1"></a>**Declarada.** No hay registro con texto libre ni cadenas de formato. `obs-principios-1`
- <a id="obs-principios-2"></a>**Explícita.** Emitir exige el efecto de telemetría; una función pura nunca emite. `obs-principios-2`
- <a id="obs-principios-3"></a>**Con procedencia.** Un dato secreto nunca es campo de telemetría. Las etiquetas que el paquete declara sensibles se excluyen, se redactan o se resumen con un hash con clave. `obs-principios-3`
- <a id="obs-principios-4"></a>**Revisable.** Las señales de un binario forman su manifiesto de telemetría, que el diff de significado compara entre versiones. `obs-principios-4`
- <a id="obs-principios-5"></a>**Ligada a la verificación.** Cada señal lleva la identidad de la definición que la emitió. `obs-principios-5`
- <a id="obs-principios-6"></a>**Estándar.** Las señales siguen el modelo de datos y las convenciones semánticas de OpenTelemetry y se exportan con OTLP; el contexto de traza entre procesos usa W3C Trace Context; los niveles de severidad son los del modelo de registros de OpenTelemetry; las unidades, las de UCUM; las marcas de tiempo, RFC 3339. `obs-principios-6`

## <a id="obs-senales"></a>Señales

| Señal                   | Contenido                                                                       |
|-------------------------|---------------------------------------------------------------------------------|
| Evento `obs-senales-1`  | Un hecho con nivel de severidad y campos tipados.                               |
| Métrica `obs-senales-2` | Contador, medidor o histograma, con unidad y atributos cuyo tipo tiene un conjunto finito y declarado de valores (enumeraciones, booleanos o enteros de rango acotado). |
| Span `obs-senales-3`    | Un intervalo de trabajo con atributos, que forma parte del contexto de traza.   |

- <a id="obs-senales-4"></a>El span activo forma parte del estado de la tarea; una tarea hija hereda el de su padre, y esa herencia es explícita en la representación intermedia. Entre procesos, el contexto de traza viaja por la frontera. `obs-senales-4`
- <a id="obs-senales-5"></a>Un campo *external* se admite y se escapa; nunca se interpreta como formato. `obs-senales-5`
- <a id="obs-senales-6"></a>Un exportador que descarta todo permite al backend eliminar las emisiones por completo. La mutación no muta las llamadas de telemetría. `obs-senales-6`
- <a id="obs-senales-7"></a>El informe de aborto se emite también como evento de máxima severidad si hay un exportador. `obs-senales-7`

## <a id="obs-pendiente"></a>Lo que queda por definir *(Informativa)*

El formato del manifiesto de telemetría (`anx-pendiente-9`). Todo está registrado en el [anexo A](33-anexo-a.md).

---

← [Entrada y salida](23-es.md) · [Índice](README.md) · [Interoperabilidad](25-interop.md) →
