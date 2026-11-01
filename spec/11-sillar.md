---
title: "Sillar"
order: 11
mark: sillar
mark_group: plat
---
*Plataforma · IR de bajo nivel*

# Sillar

**Rol:** IR de bajo nivel · **Existe:** solo en compilación

Sillar es la representación de bajo nivel entre Stela verificada y el código del destino. Cincel la produce al bajar Stela, Pulido la optimiza y Plomada valida cada pasada de optimización.

## <a id="sillar-forma"></a>Forma

- <a id="sillar-forma-1"></a>Forma de asignación única estática (SSA) sobre un grafo de control: cada valor se define una sola vez. `sillar-forma-1`
- <a id="sillar-forma-2"></a>Los valores que llegan a un bloque desde varios predecesores, como las variables de un bucle, se pasan como argumentos de bloque; no hay nodos phi. `sillar-forma-2`
- <a id="sillar-forma-3"></a>Cada instrucción define como máximo un valor y recibe operandos explícitos. `sillar-forma-3`
- <a id="sillar-forma-4"></a>Cada bloque termina en exactamente un terminador: salto, bifurcación condicional, retorno o aborto declarado. `sillar-forma-4`
- <a id="sillar-forma-5"></a>Usa los tipos de máquina y el modelo de memoria del destino que declara su especificación ([Rumbo](19-rumbo.md)). `sillar-forma-5`
- <a id="sillar-forma-6"></a>Existe solo en compilación (R3): nunca se distribuye ni se ejecuta. `sillar-forma-6`

## <a id="sillar-anotaciones"></a>Anotaciones obligatorias

<a id="sillar-anotaciones-1"></a>Sillar conserva como anotaciones explícitas todo lo que una optimización DEBE respetar: `sillar-anotaciones-1`

- <a id="sillar-anotaciones-2"></a>los datos secretos y la disciplina de tiempo constante; `sillar-anotaciones-2`
- <a id="sillar-anotaciones-3"></a>las protecciones de especulación; `sillar-anotaciones-3`
- <a id="sillar-anotaciones-4"></a>los borrados de secretos; `sillar-anotaciones-4`
- <a id="sillar-anotaciones-5"></a>los puntos de telemetría; `sillar-anotaciones-5`
- <a id="sillar-anotaciones-6"></a>los límites de los efectos. `sillar-anotaciones-6`

## <a id="sillar-semantica"></a>Semántica

- <a id="sillar-semantica-1"></a>La semántica de Sillar es operacional y DEBE mecanizarse en un asistente de pruebas, como la de Stela; ante cualquier diferencia con esta descripción, prevalece la mecanización. `sillar-semantica-1`
- <a id="sillar-semantica-2"></a>La semántica de Sillar sustenta dos garantías: T7, que relaciona la semántica de Stela con la de Sillar y la del destino a través de la bajada y del resto del núcleo de Cincel, y T8, que relaciona la entrada y la salida de cada pasada que valida Plomada. `sillar-semantica-2`

## <a id="sillar-pulido"></a>Técnicas internas de las pasadas

- <a id="sillar-pulido-1"></a>Sillar es la forma de intercambio entre pasadas. Una pasada PUEDE usar internamente cualquier otra representación o técnica, como grafos de nodos o grafos de equivalencia. `sillar-pulido-1`
- <a id="sillar-pulido-2"></a>Lo que una pasada entrega DEBE ser Sillar, y pasa por Plomada; si no pasa, la pasada pertenece a la TCB y se declara en el inventario de confianza (R9). `sillar-pulido-2`

## <a id="sillar-concreto"></a>Lo que queda por definir

<a id="sillar-concreto-1"></a>Su codificación concreta, textual o binaria, se define en la etapa siguiente, sin contradecir estos requisitos. DEBE ser determinista, para que la construcción sea reproducible ([anexo A](33-anexo-a.md)). `sillar-concreto-1`

---

← [Stela](10-stela.md) · [Índice](README.md) · [Dintel](12-dintel.md) →
