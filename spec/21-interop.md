<!-- SPDX-FileCopyrightText: 2026 Xhunik Nikol Miguel Mutzutz y colaboradores de Dubito -->
<!-- SPDX-License-Identifier: CC-BY-SA-4.0 -->

*Plataforma*

# Interoperabilidad

Hay cuatro relaciones posibles: entre lenguajes de la familia, con el resto del sistema por la convención de llamada de la plataforma, con código nativo no verificado y con componentes externos a través de una frontera asíncrona.

## <a id="int-familia"></a>Entre lenguajes de la familia

<a id="int-familia-1"></a>Un módulo importa a otro en cualquier lenguaje, y la llamada conserva efectos, contratos y etiquetas sin convertir datos. `int-familia-1`

- <a id="int-familia-2"></a>Una función de Solsticio exportada no deja efectos del usuario sin manejar. `int-familia-2`
- <a id="int-familia-3"></a>Una función de Voluta se ve con el tipo que declara; sus esquemas son registros y sus uniones de claves, tipos suma. `int-familia-3`
- <a id="int-familia-4"></a>Una salida de Amate se ve como una función que recibe relaciones y devuelve otra. `int-familia-4`
- <a id="int-familia-5"></a>Un actor de Relevo se ve como su dirección, con envío y consulta como funciones. `int-familia-5`
- <a id="int-familia-6"></a>Las clases de Talud se ven como registros con su tabla de métodos, y sus objetos como objetos de trait. `int-familia-6`

## <a id="int-export"></a>Hacia afuera

- <a id="int-export-1"></a>Una función exportada usa la convención de llamada que declara el destino. Solo cruzan tipos de frontera: escalares, registros y arreglos con layout definido, y vistas como dirección y longitud. `int-export-1`
- <a id="int-export-2"></a>Sus precondiciones se comprueban en la entrada, porque quien llama no está verificado, y todo lo que recibe es *external*. `int-export-2`
- <a id="int-export-3"></a>Se genera una descripción de la interfaz (firmas, tipos de frontera y contratos como documentación) para que otros ecosistemas generen su lado. `int-export-3`
- <a id="int-export-4"></a>Cargada en un proceso no verificado, su garantía es condicional al anfitrión; como servicio deja de serlo ([Bibliotecas exportadas](14-confianza.md#conf-exportadas)). `int-export-4`

## <a id="int-nativo"></a>Código nativo importado

- <a id="int-nativo-1"></a>El código nativo no verificado se declara con sus funciones y se ejecuta fuera de la memoria del programa, con un modo de aislamiento que admita el destino; si no admite ninguno, la declaración se rechaza. `int-nativo-1`
- <a id="int-nativo-2"></a>Cada función recibe tipos de frontera y devuelve un resultado con error cuyo valor es *external*. `int-nativo-2`
- <a id="int-nativo-3"></a>Los argumentos se copian al compartimento y los resultados de vuelta; no hay préstamos ni memoria compartida. `int-nativo-3`
- <a id="int-nativo-4"></a>Llamar exige el efecto de código nativo y los efectos que la declaración autoriza; el compartimento recibe permiso solo para esos efectos. `int-nativo-4`
- <a id="int-nativo-5"></a>Si el compartimento cae, excede su memoria o su plazo, la llamada devuelve error y el compartimento se reinicia. `int-nativo-5`
- <a id="int-nativo-6"></a>El canal entre programa y compartimento es una frontera asíncrona con caída, retraso y corrupción; el programa valida cada respuesta antes de convertirla en valor. `int-nativo-6`

### <a id="int-callbacks"></a>Callbacks

- <a id="int-nativo-7"></a>Una biblioteca nativa solo puede llamar al programa a través de callbacks declarados, cada uno con su firma, sus efectos y la función del programa que lo implementa. `int-nativo-7`
- <a id="int-nativo-8"></a>Un callback solo puede invocarse mientras una llamada del programa a esa biblioteca está en curso, y se atiende en ese punto, como un mensaje. `int-nativo-8`
- <a id="int-nativo-9"></a>Sus argumentos llegan como *external* y se validan. Dentro de un callback no se puede llamar a la misma biblioteca. `int-nativo-9`
- <a id="int-nativo-10"></a>El callback es código verificado del programa; el código nativo no gana permisos al invocarlo. `int-nativo-10`

## <a id="int-plugins"></a>Plugins

- <a id="int-plugins-1"></a>Un binario declara cada punto de extensión con un trait con contratos, un techo de efectos y un techo de confianza, que quedan en su atestación. `int-plugins-1`
- <a id="int-plugins-2"></a>Un plugin es un módulo compilado para el mismo destino, con atestación que demuestra que implementa el trait dentro de ambos techos e incluye la identidad del código generado. `int-plugins-2`
- <a id="int-plugins-3"></a>Cargarlo exige su efecto y comprueba la firma, la identidad del código, del destino y de la interfaz, y las identidades aceptadas; no compila ni verifica nada en ejecución. `int-plugins-3`
- <a id="int-plugins-4"></a>Un plugin vive hasta que termina el ámbito que lo cargó. `int-plugins-4`
- <a id="int-plugins-5"></a>El cargador y cada techo figuran en el inventario de confianza. Un plugin no verificado solo se carga como código nativo aislado. `int-plugins-5`

## <a id="int-par"></a>Par externo

- <a id="int-par-1"></a>Un componente de cualquier lenguaje, en cualquier lugar, puede tratarse como un par al otro lado de una frontera asíncrona. Es la opción de mayor aislamiento: sin memoria ni proceso compartidos, las garantías del programa valen sin condiciones. `int-par-1`
- <a id="int-par-2"></a>La interfaz se publica como documento AsyncAPI 3.1.0, con los mensajes en CBOR determinista y sus esquemas en CDDL; los contratos, la idempotencia y el modelo de fallos van como extensiones de la especificación. Otros ecosistemas generan su lado a partir de ese documento. `int-par-2`
- <a id="int-par-3"></a>Lo que se envía se demuestra contra las precondiciones del otro lado; lo que se recibe es *external* y las postcondiciones del otro lado se comprueban al recibir, fuera de la política de comprobaciones. `int-par-3`
- <a id="int-par-4"></a>**Par verificado.** Si el otro lado es un binario de la familia y presenta una atestación aceptada con la misma interfaz, lo que llega es *peer* y sus postcondiciones se asumen. Esa suposición figura en el inventario de confianza. `int-par-4`

## <a id="int-sistema"></a>Biblioteca del sistema

<a id="int-sistema-1"></a>La biblioteca del sistema no se importa como código nativo: la usa std en la base del sistema, con sus funciones declaradas en la especificación del destino y enumeradas en el inventario. Las marcadas como aisladas usan el mismo canal que el código nativo. `int-sistema-1`

---

← [Observabilidad](20-observabilidad.md) · [Índice](README.md) · [Ceiba](22-ceiba.md) →
