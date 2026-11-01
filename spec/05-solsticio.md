---
title: "Solsticio"
order: 5
mark: solsticio
mark_group: lang
---
*Lenguaje funcional*

# Solsticio

**Paradigma:** funcional puro · **Perfiles:** core, freestanding, hosted

Solsticio es el lenguaje funcional puro de la familia: todo es una expresión, no existe la mutación y los efectos del usuario se describen como operaciones con manejadores.

## <a id="cyc-clasificacion"></a>Clasificación

| Eje                                | Solsticio                                                            |
|------------------------------------|----------------------------------------------------------------------|
| <a id="cyc-clasificacion-1"></a>Paradigma `cyc-clasificacion-1`    | Funcional puro                                                       |
| <a id="cyc-clasificacion-2"></a>Memoria `cyc-clasificacion-2`      | Valores inmutables; compartición resuelta al compilar                |
| <a id="cyc-clasificacion-3"></a>Evaluación `cyc-clasificacion-3`   | Estricta, con pereza explícita                                       |
| <a id="cyc-clasificacion-4"></a>Efectos `cyc-clasificacion-4`      | Efectos de la plataforma y efectos del usuario con manejadores       |
| <a id="cyc-clasificacion-5"></a>Totalidad `cyc-clasificacion-5`    | Total por defecto; recursión general con el efecto de no terminación |
| <a id="cyc-clasificacion-6"></a>Polimorfismo `cyc-clasificacion-6` | Paramétrico y por traits                                             |
| <a id="cyc-clasificacion-7"></a>Despacho `cyc-clasificacion-7`     | Estático; las funciones son valores                                  |
| <a id="cyc-clasificacion-8"></a>Concurrencia `cyc-clasificacion-8` | Paralelismo de expresiones puras y tareas                            |

## <a id="cyc-modelo"></a>Modelo

- <a id="cyc-modelo-1"></a>**Valores.** Semánticamente todo valor se copia. El compilador decide la representación: los que escapan o se comparten usan conteo de referencias, y una actualización sobre un valor con una sola referencia se hace en el lugar. Sin mutación ni valores que dependan de sí mismos no hay ciclos, así que el conteo libera toda la memoria. `cyc-modelo-1`
- <a id="cyc-modelo-2"></a>**Tipos algebraicos.** Sumas de variantes con campos nombrados y registros. La copia con campos cambiados es una operación explícita. `cyc-modelo-2`
- <a id="cyc-modelo-3"></a>**Funciones.** Su cuerpo es una expresión. Las funciones anónimas declaran sus tipos y capturan por valor. Las llamadas en posición de cola nunca hacen crecer la pila. `cyc-modelo-3`
- <a id="cyc-modelo-4"></a>**Pereza.** Un valor diferido se evalúa la primera vez que se pide y guarda su resultado; la expresión diferida no puede tener efectos ni depender, directa o indirectamente, del propio valor diferido. Una estructura infinita se describe con una función que produce cada parte al pedirla. `cyc-modelo-4`
- <a id="cyc-modelo-5"></a>**Todo valor es transferible y compartible**, porque es inmutable. `cyc-modelo-5`

## <a id="cyc-manejadores"></a>Efectos del usuario

- <a id="cyc-manejadores-1"></a>Un efecto del usuario declara operaciones. Una operación normal reanuda el cálculo con un valor; una operación de aborto no reanuda. `cyc-manejadores-1`
- <a id="cyc-manejadores-2"></a>Un manejador da significado a las operaciones dentro de una expresión y puede llevar parámetros que se actualizan en cada reanudación, y una cláusula que transforma el resultado final. `cyc-manejadores-2`
- <a id="cyc-manejadores-3"></a>La reanudación aparece como máximo una vez por cláusula y en posición de cola: nunca se guarda una continuación y no hace falta soporte en ejecución. `cyc-manejadores-3`
- <a id="cyc-manejadores-4"></a>Una función exportada a otro lenguaje no puede dejar efectos del usuario sin manejar. `cyc-manejadores-4`
- <a id="cyc-manejadores-5"></a>Los errores pueden expresarse como resultado con error o como un efecto de fallo con su manejador; la representación intermedia ve siempre el resultado con error. `cyc-manejadores-5`

## <a id="cyc-especificos"></a>Contratos, concurrencia y pruebas

- <a id="cyc-especificos-1"></a>Como no hay estado, los contratos no tienen valores de entrada. La pureza permite usar cualquier función total como término de un contrato, y los lemas sobre funciones recursivas se demuestran por inducción. `cyc-especificos-1`
- <a id="cyc-especificos-2"></a>La evaluación paralela de expresiones puras devuelve el mismo resultado que la secuencial y exige el efecto de tareas. `cyc-especificos-2`
- <a id="cyc-especificos-3"></a>La E/S devuelve valores nuevos en lugar de modificar buffers. `cyc-especificos-3`
- <a id="cyc-especificos-4"></a>Una prueba con un cuantificador se ejecuta como prueba de propiedades sobre valores generados. `cyc-especificos-4`

## <a id="cyc-pendiente"></a>Lo que queda por definir *(Informativa)*

La sintaxis concreta (`anx-pendiente-1`), que se elige según la [elección de la sintaxis](01-familia.md#fam-eleccion), y los nombres de su biblioteca de soporte (`anx-pendiente-7`). Todo está registrado en el [anexo A](33-anexo-a.md).

---

← [Talud](04-talud.md) · [Índice](README.md) · [Voluta](06-voluta.md) →
