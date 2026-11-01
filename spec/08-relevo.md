---
title: "Relevo"
order: 8
mark: relevo
mark_group: lang
---
*Lenguaje de actores*

# Relevo

**Paradigma:** actores · **Perfiles:** core, freestanding, hosted

Relevo organiza un programa en actores: unidades aisladas con estado propio que solo se comunican por mensajes y que se organizan en árboles de supervisión. Un mensaje mueve su contenido, así que nunca hay memoria compartida, y el fallo de un actor libera su región sin afectar al resto del proceso.

## <a id="rel-clasificacion"></a>Clasificación

| Eje                                | Relevo                                                 |
|------------------------------------|--------------------------------------------------------|
| <a id="rel-clasificacion-1"></a>Paradigma `rel-clasificacion-1`    | Actores con supervisión                                |
| <a id="rel-clasificacion-2"></a>Memoria `rel-clasificacion-2`      | Una región por actor; los mensajes mueven su contenido |
| <a id="rel-clasificacion-3"></a>Evaluación `rel-clasificacion-3`   | Estricta; un mensaje a la vez por actor                |
| <a id="rel-clasificacion-4"></a>Concurrencia `rel-clasificacion-4` | Actores sobre el motor de tareas                       |

## <a id="rel-actores"></a>Actores y mensajes

- <a id="rel-actores-1"></a>Un actor declara sus parámetros de creación, un buzón de capacidad acotada, su estado, su invariante y un manejador por mensaje, con o sin respuesta. `rel-actores-1`
- <a id="rel-actores-2"></a>La dirección de un actor es un valor pequeño, copiable, transferible y compartible, que no lo mantiene vivo. Todo lo que viaja en un mensaje es transferible. `rel-actores-2`
- <a id="rel-actores-3"></a>Enviar a un buzón lleno suspende al emisor; existe un envío que no espera y devuelve error. Una consulta envía, espera la respuesta y exige plazo; su resultado distingue respuesta, plazo vencido y actor caído. Un mensaje puede programarse a futuro. `rel-actores-3`
- <a id="rel-actores-4"></a>Los mensajes de un mismo emisor a un mismo receptor llegan en orden de envío. Un actor procesa sus mensajes de uno en uno; su estado nunca se observa a medias. `rel-actores-4`
- <a id="rel-actores-5"></a>Cada actor asigna de su propia región y no tiene préstamos hacia otra; al terminar o fallar, su región se libera completa. Los valores inmutables compartibles con conteo de referencias pueden enviarse sin copiar su contenido. `rel-actores-5`

## <a id="rel-supervision"></a>Supervisión

- <a id="rel-supervision-1"></a>Todo actor tiene un supervisor, y ninguno sobrevive al árbol que lo creó. `rel-supervision-1`
- <a id="rel-supervision-2"></a>Estrategias: reiniciar solo el hijo que falló, todos los hijos, o ese hijo y los declarados después de él. `rel-supervision-2`
- <a id="rel-supervision-3"></a>Políticas por hijo: reiniciar siempre, solo si falló, o nunca. Superar un máximo de reinicios en una ventana de tiempo hace fallar al supervisor; si falla el raíz, el proceso aborta con el informe del último fallo. `rel-supervision-3`

## <a id="rel-contratos"></a>Contratos, errores y esperas

- <a id="rel-contratos-1"></a>Cada manejador declara precondiciones y postcondiciones sobre sus argumentos y el estado, con acceso al estado al empezar el mensaje. La invariante del actor es pre y postcondición de todo manejador. Las precondiciones se verifican en el punto de envío o consulta. `rel-contratos-1`
- <a id="rel-contratos-2"></a>Una extensión fantasma da a un actor campos que modelan su historia, y una actualización fantasma fija cómo cambian al terminar cada manejador. `rel-contratos-2`
- <a id="rel-contratos-3"></a>Un manejador con respuesta puede devolver un error, que llega a quien consultó; el actor continúa. Una comprobación en ejecución que falla dentro de un manejador termina ese actor con aborto por región: sus mensajes pendientes se descartan, sus consultas pendientes reciben actor caído y su supervisor recibe el informe. `rel-contratos-3`
- <a id="rel-contratos-4"></a>El grafo de esperas entre tipos de actor (consultas y envíos que se suspenden con buzón lleno) es acíclico. Dentro de un ciclo de envíos se usa el envío que no espera. `rel-contratos-4`
- <a id="rel-contratos-5"></a>Los efectos de un actor son la unión de los de sus manejadores y aparecen en su interfaz. `rel-contratos-5`
- <a id="rel-contratos-6"></a>Con el motor simulado, una prueba puede inyectar fallos en actores concretos para comprobar la supervisión. `rel-contratos-6`

## <a id="rel-remotos"></a>Actores remotos

<a id="rel-remotos-1"></a>Un actor de otro proceso o de otra máquina se alcanza a través de una [frontera asíncrona](02-nucleo.md#nuc-fronteras), y nada lo oculta: `rel-remotos-1`

- <a id="rel-remotos-2"></a>Un actor remoto tiene un tipo de dirección distinto del de un actor local. Un supervisor puede publicar un hijo con un nombre, y otro nodo lo busca a través de una frontera. No se crean actores en otro nodo. `rel-remotos-2`
- <a id="rel-remotos-3"></a>El contenido de los mensajes es codificable y viaja con la codificación canónica. Lo que llega es *external*, o *peer* si el otro nodo es un par verificado. `rel-remotos-3`
- <a id="rel-remotos-4"></a>Los mensajes entre dos actores viajan en una sesión: llegan en orden, con posibles huecos si el transporte pierde mensajes. `rel-remotos-4`
- <a id="rel-remotos-5"></a>Un envío remoto entrega como máximo una vez; con reintento entrega al menos una vez, y solo se admite hacia manejadores idempotentes. `rel-remotos-5`
- <a id="rel-remotos-6"></a>Una consulta remota exige plazo, y su resultado distingue además destino inalcanzable y resultado desconocido. `rel-remotos-6`
- <a id="rel-remotos-7"></a>Un supervisor puede vigilar un actor remoto y recibe una sospecha cuando no responde dentro del plazo. `rel-remotos-7`
- <a id="rel-remotos-8"></a>Las consultas remotas no forman parte del grafo de esperas; su plazo obligatorio acota toda espera. `rel-remotos-8`

## <a id="rel-pendiente"></a>Lo que queda por definir *(Informativa)*

La sintaxis concreta (`anx-pendiente-1`), que se elige según la [elección de la sintaxis](01-familia.md#fam-eleccion), y los nombres de su biblioteca de soporte (`anx-pendiente-7`). Todo está registrado en el [anexo A](33-anexo-a.md).

---

← [Amate](07-amate.md) · [Índice](README.md) · [dubito](09-compilador.md) →
