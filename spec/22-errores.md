---
title: "Errores y aborto"
order: 22
---
*Plataforma*

# Errores y aborto

**Rol:** clases de fallo, errores como valores y aborto · **En la TCB:** no

La plataforma distingue lo que puede salir mal en un programa correcto, que es un valor que el programa maneja, de lo que solo puede ocurrir si una afirmación no demostrada resulta falsa, que detiene la ejecución. No hay excepciones, desenrollado de pila ni recuperación oculta.

## <a id="err-clases"></a>Clases de fallo

| Clase                                   | Ejemplo                                                   | Representación                                            |
|-----------------------------------------|-----------------------------------------------------------|-----------------------------------------------------------|
| Error esperable `err-clases-1`          | Archivo inexistente, saldo insuficiente, conexión cerrada | Valor de error de un resultado                            |
| Obligación no demostrada `err-clases-2` | Una comprobación en ejecución que resulta falsa           | Aborto del proceso o de la región                         |
| Agotamiento de recursos `err-clases-3`  | Memoria insuficiente                                      | Aborto, salvo en operaciones que lo ofrecen como error    |
| Fallo de una frontera `err-clases-4`    | Código nativo que cae, plazo vencido, mensaje corrupto    | Valor de error con las variantes de los fallos declarados |
| Cancelación `err-clases-5`              | Una tarea cuyo ámbito se cierra antes de que termine      | Valor de error en su siguiente operación de espera        |

## <a id="err-valores"></a>Errores como valores

- <a id="err-valores-1"></a>Un error es un valor de un tipo declarado. No lleva traza ni mensaje salvo que su tipo los incluya. `err-valores-1`
- <a id="err-valores-2"></a>Ignorar un resultado con error es un error de compilación; descartarlo es explícito. `err-valores-2`
- <a id="err-valores-3"></a>La propagación no convierte tipos por su cuenta; envolver un error es explícito. `err-valores-3`
- <a id="err-valores-4"></a>Un tipo de error puede acumular los puntos de propagación por los que pasa. `err-valores-4`
- <a id="err-valores-5"></a>Los contratos describen los errores: qué es cierto cuando la función falla. `err-valores-5`
- <a id="err-valores-6"></a>Los errores del sistema operativo tienen una categoría portable y el código original del sistema, que es *external*. `err-valores-6`

## <a id="err-aborto"></a>Aborto

- <a id="err-aborto-1"></a>Si una comprobación en ejecución falla, la ejecución se detiene sin ejecutar más código del programa: sin desenrollado, destructores ni manejadores. `err-aborto-1`
- <a id="err-aborto-2"></a>**Hosted:** se emite el informe de aborto y el proceso termina como define el destino. `err-aborto-2`
- <a id="err-aborto-3"></a>**Freestanding:** se invoca el manejador que declara el paquete raíz, que recibe el informe y no puede retornar. `err-aborto-3`
- <a id="err-aborto-4"></a>**Por región:** en un programa cuya memoria está dividida en regiones sin préstamos entre ellas, el destino puede limitar el aborto a una región, que se libera completa mientras el resto continúa. `err-aborto-4`
- <a id="err-aborto-5"></a>El informe de aborto se emite como registro del modelo de datos de OpenTelemetry. Contiene la VC que falló y su clase, la identidad de la definición y del módulo, la posición en el código fuente, los operandos de la VC salvo los secretos y los sensibles, la tarea o actor y el contexto de traza, y si el aborto fue del proceso o de una región. Lo genera el destino sin ejecutar código del programa. `err-aborto-5`

## <a id="err-pendiente"></a>Lo que queda por definir *(Informativa)*

Los campos propios del informe de aborto, más allá del modelo de registros de OpenTelemetry (`anx-pendiente-9`), y, por destino, la semántica del aborto (`anx-destino-10`). Todo está registrado en el [anexo A](33-anexo-a.md).

---

← [Chinampa](21-chinampa.md) · [Índice](README.md) · [Entrada y salida](23-es.md) →
