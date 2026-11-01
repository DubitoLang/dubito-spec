---
title: "Speculum"
order: 14
mark: speculum
mark_group: plat
---
*Plataforma · mutación*

# Speculum

**Rol:** pruebas de mutación · **En la TCB:** no

Speculum mide la adecuación de las especificaciones. Introduce mutaciones en el cuerpo de una función y comprueba qué mutantes detecta cada postcondición. Una postcondición que no elimina ningún mutante no afirma nada sobre la implementación y se rechaza (R5).

## <a id="elk-op"></a>Mutaciones

<a id="elk-op-1"></a>Los operadores del conjunto suficiente de la literatura de pruebas de mutación (Offutt, Lee, Rothermel, Untch y Zapf, 1996): reemplazo de operadores aritméticos, relacionales y lógicos; reemplazo de constantes; desplazamiento de límites; eliminación de sentencias; intercambio de argumentos del mismo tipo. Se aplican sobre la representación intermedia, así que valen para cualquier lenguaje. `elk-op-1`

## <a id="elk-sel"></a>Selección

- <a id="elk-sel-1"></a>Solo se mutan definiciones nuevas o modificadas, identificadas por su identidad. `elk-sel-1`
- <a id="elk-sel-2"></a>No se mutan las llamadas de telemetría, las funciones derivadas ni el código fantasma. `elk-sel-2`
- <a id="elk-sel-3"></a>Un mutante se descarta como equivalente solo si es idéntico al original tras la compilación o si su equivalencia se demuestra con certificado. Como la equivalencia es indecidible, un mutante sin ese certificado cuenta como sobreviviente. `elk-sel-3`

## <a id="elk-criterio"></a>Criterio de aceptación

- <a id="elk-criterio-1"></a>**Eliminación.** Un mutante queda eliminado solo con un contraejemplo concreto: una entrada, obtenida de un modelo del solucionador o de una prueba que falla, con la que el mutante incumple la postcondición. El contraejemplo forma parte de la evidencia y se comprueba evaluando el mutante sobre esa entrada con la semántica de Stela, con un presupuesto determinista de pasos y sin generar código del destino. Si el mutante invoca intrínsecos, el contraejemplo incluye además la respuesta de cada invocación, que DEBE cumplir el contrato del intrínseco en la especificación del destino. Que no pueda demostrarse su postcondición no lo elimina. `elk-criterio-1`
- <a id="elk-criterio-2"></a>**Por postcondición.** Cada postcondición de código ejecutable DEBE eliminar al menos un mutante. `elk-criterio-2`
- <a id="elk-criterio-3"></a>**Puntuación.** Mutantes eliminados entre mutantes sin certificado de equivalencia. El paquete puede fijar un mínimo. `elk-criterio-3`
- <a id="elk-criterio-4"></a>**Determinismo.** El conjunto de mutantes depende solo de la definición y de la versión de la herramienta; cualquiera puede repetirlo. `elk-criterio-4`

## <a id="elk-pendiente"></a>Lo que queda por definir *(Informativa)*

El formato de la evidencia de mutación (`anx-pendiente-5`) y, por implementación, la selección de mutantes dentro de los operadores adoptados (`anx-implementacion-4`). Todo está registrado en el [anexo A](33-anexo-a.md).

---

← [Plomada](13-plomada.md) · [Índice](README.md) · [Pulido](15-pulido.md) →
