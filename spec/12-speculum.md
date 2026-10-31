<!-- SPDX-FileCopyrightText: 2026 Xhunik Nikol Miguel Mutzutz y colaboradores de Dubito -->
<!-- SPDX-License-Identifier: CC-BY-SA-4.0 -->

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

- <a id="elk-criterio-1"></a>**Eliminación.** Un mutante queda eliminado solo con un contraejemplo concreto: un modelo del solucionador en el que incumple la postcondición, o una prueba que falla. Que no pueda demostrarse su postcondición no lo elimina. `elk-criterio-1`
- <a id="elk-criterio-2"></a>**Por postcondición.** Cada postcondición de código ejecutable DEBE eliminar al menos un mutante. `elk-criterio-2`
- <a id="elk-criterio-3"></a>**Puntuación.** Mutantes eliminados entre mutantes sin certificado de equivalencia. El paquete puede fijar un mínimo. `elk-criterio-3`
- <a id="elk-criterio-4"></a>**Determinismo.** El conjunto de mutantes depende solo de la definición y de la versión de la herramienta; cualquiera puede repetirlo. `elk-criterio-4`

---

← [Dintel](11-dintel.md) · [Índice](README.md) · [Destinos](13-destinos.md) →
