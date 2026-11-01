---
title: "Núcleo común"
order: 2
---
*Introducción*

# Núcleo común

Lo que los seis lenguajes comparten no pertenece a ninguno de ellos. Aquí se define una sola vez; cada lenguaje decide cómo se escribe.

## <a id="nuc-tipos"></a>Tipos

<a id="nuc-tipos-1"></a>Rige R10: todo nombre que se introduce declara su tipo, y toda instanciación genérica, incluidas las de efectos, se escribe. Una expresión se comprueba contra el tipo esperado; un literal sin tipo propio toma el del lugar donde aparece, y si ese lugar no lo fija es un error. `nuc-tipos-1`

| Categoría                                 | Definición                                                                                                                                                                                                                                 |
|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <a id="nuc-tipos-2"></a>Enteros `nuc-tipos-2`                     | Con signo y sin signo, de ancho fijo. Ver [Aritmética numérica](#nuc-numeros).                                                                                                                                                             |
| <a id="nuc-tipos-3"></a>Punto flotante `nuc-tipos-3`              | Binarios de precisión simple y doble según IEEE 754.                                                                                                                                                                                       |
| <a id="nuc-tipos-4"></a>Decimales `nuc-tipos-4`                   | Aritmética decimal de IEEE 754-2019 (formato decimal128), con escala fija por tipo.                                                                                                                                                        |
| <a id="nuc-tipos-5"></a>Otros escalares `nuc-tipos-5`             | Booleano, escalar Unicode, unidad y el tipo vacío, sin valores.                                                                                                                                                                            |
| <a id="nuc-tipos-6"></a>Registros `nuc-tipos-6`                   | Productos con campos nombrados. El layout lo define la especificación del destino.                                                                                                                                                         |
| <a id="nuc-tipos-7"></a>Tipos suma `nuc-tipos-7`                  | Siempre etiquetados; su inspección es exhaustiva.                                                                                                                                                                                          |
| <a id="nuc-tipos-8"></a>Opcionales y resultados `nuc-tipos-8`     | Tipos suma de la plataforma. No hay valores nulos ni excepciones.                                                                                                                                                                          |
| <a id="nuc-tipos-9"></a>Tuplas `nuc-tipos-9`                      | Productos sin nombres; la tupla vacía es la unidad.                                                                                                                                                                                        |
| <a id="nuc-tipos-10"></a>Arreglos y vistas `nuc-tipos-10`          | Arreglos de longitud fija y vistas sobre secuencias contiguas. Todo acceso indexado genera la VC de límites.                                                                                                                               |
| <a id="nuc-tipos-11"></a>Préstamos `nuc-tipos-11`                  | Compartidos e inmutables, o exclusivos y mutables. Nunca nulos.                                                                                                                                                                            |
| <a id="nuc-tipos-12"></a>Funciones `nuc-tipos-12`                  | Los nombres de los parámetros y los efectos son parte del tipo.                                                                                                                                                                            |
| <a id="nuc-tipos-13"></a>Genéricos `nuc-tipos-13`                  | Parámetros de tipo, de efecto y constantes; se monomorfizan en compilación.                                                                                                                                                                |
| <a id="nuc-tipos-14"></a>Objetos de trait `nuc-tipos-14`           | Valores de tipo desconocido que implementan un trait, solo detrás de un préstamo o de un dueño.                                                                                                                                            |
| <a id="nuc-tipos-15"></a>Procedencia `nuc-tipos-15`                | Cualquier tipo puede llevar una etiqueta. Ver [Procedencia](#nuc-procedencia).                                                                                                                                                             |
| <a id="nuc-tipos-16"></a>Capacidades `nuc-tipos-16`                | Testigos de tamaño cero de que una extensión del procesador está disponible.                                                                                                                                                               |
| <a id="nuc-tipos-17"></a>Datos de forma desconocida `nuc-tipos-17` | Un tipo suma ordinario que representa exactamente el modelo de datos de CBOR (RFC 8949), que incluye el de JSON (RFC 8259). Se examina de forma exhaustiva o se convierte a un tipo concreto con una operación explícita que puede fallar. |
| <a id="nuc-tipos-18"></a>Texto `nuc-tipos-18`                      | Texto Unicode validado. No se indexa por entero: se recorre por escalares o por su codificación.                                                                                                                                           |

<a id="nuc-tipos-19"></a>No hay conversiones implícitas. Ampliar sin pérdida, reducir con la VC de que el valor cabe, truncar y convertir con resultado opcional son operaciones distintas y explícitas. `nuc-tipos-19`

### <a id="nuc-tipos-constantes"></a>Parámetros constantes

- <a id="nuc-tipos-20"></a>Un parámetro genérico constante recibe un valor entero. Un argumento constante es una expresión sobre literales enteros y parámetros constantes con suma, resta y multiplicación; no se admiten división, llamadas ni comparaciones. `nuc-tipos-20`
- <a id="nuc-tipos-21"></a>**Igualdad.** Dos tipos con argumentos constantes son iguales si sus expresiones tienen la misma forma normal como polinomio con coeficientes enteros. Comparar formas normales es decidible. `nuc-tipos-21`
- <a id="nuc-tipos-22"></a>**Restricciones.** Las condiciones sobre parámetros constantes son precondiciones del genérico y se comprueban al instanciarlo, cuando todos los valores son conocidos. `nuc-tipos-22`
- <a id="nuc-tipos-23"></a>**Evaluación.** Con enteros sin cota; el resultado DEBE caber en el tipo del parámetro. `nuc-tipos-23`

## <a id="nuc-numeros"></a>Aritmética numérica

<a id="nuc-numeros-1"></a>Enteros, flotantes y decimales tienen una semántica exacta e idéntica en todo destino: el mismo programa con las mismas entradas produce los mismos bits en cualquier máquina. Ninguna operación redondea, desborda ni produce un valor especial sin que el programa lo pida. `nuc-numeros-1`

### <a id="nuc-numeros-enteros"></a>Enteros

<a id="nuc-numeros-2"></a>Por defecto, cada operación genera la VC de que el resultado cabe en el tipo, y cada división, la de que el divisor no es cero. La aritmética modular, comprobada o saturada se pide con operaciones explícitas. En un contrato, los enteros son enteros matemáticos. `nuc-numeros-2`

### <a id="nuc-numeros-flotante"></a>Punto flotante

- <a id="nuc-numeros-3"></a>**Formato.** Redondeo al par más cercano como único modo. No hay cambio de modo, excepciones con trampa, precisión extendida, contracción de operaciones ni descarte de subnormales; la multiplicación con suma fusionada solo existe como operación explícita. `nuc-numeros-3`
- <a id="nuc-numeros-4"></a>**Finitud.** Por defecto, cada operación genera la VC de que el resultado es finito. Existen variantes explícitas que devuelven cualquier valor de IEEE 754, incluidos infinitos y un único NaN canónico. `nuc-numeros-4`
- <a id="nuc-numeros-5"></a>**Igualdad y orden.** Las comparaciones son las de IEEE 754. Como no son reflexivas con NaN, los flotantes no implementan los traits de igualdad, orden ni hash, y un tipo con un campo flotante no puede derivarlos. El orden total de IEEE 754 está disponible de forma explícita. `nuc-numeros-5`
- <a id="nuc-numeros-6"></a>**Funciones elementales.** Las operaciones que IEEE 754-2019 exige exactas lo son, y las funciones elementales de su cláusula 9 están correctamente redondeadas en todo destino. `nuc-numeros-6`
- <a id="nuc-numeros-7"></a>**En contratos.** El solucionador razona sobre flotantes con precisión de bit. Para propiedades de análisis numérico, un flotante finito se convierte al tipo matemático de los reales, y la plataforma aporta el lema del modelo estándar de error de redondeo. `nuc-numeros-7`

### <a id="nuc-numeros-decimal"></a>Decimales

- <a id="nuc-numeros-8"></a>**Formato.** La aritmética decimal de IEEE 754-2019. La escala fija de un tipo es una restricción sobre el exponente que el compilador mantiene; ninguna operación produce un resultado fuera de la escala de su tipo sin un redondeo explícito. `nuc-numeros-8`
- <a id="nuc-numeros-9"></a>**Operaciones exactas.** Suma, resta y comparación entre decimales de la misma escala, y multiplicación por un entero, con la VC de desbordamiento. El producto de dos decimales es exacto y su escala es la suma de las escalas. `nuc-numeros-9`
- <a id="nuc-numeros-10"></a>**Redondeo explícito.** Reducir la escala o dividir exige uno de los atributos de dirección de redondeo de IEEE 754-2019: al más cercano con empate al par, al más cercano con empate lejos de cero, hacia el infinito positivo, hacia el infinito negativo o hacia cero. La división genera además la VC de divisor distinto de cero. `nuc-numeros-10`
- <a id="nuc-numeros-11"></a>**Conversiones.** Siempre explícitas y con modo de redondeo cuando hay pérdida. Convertir un flotante exige la VC de que es finito. `nuc-numeros-11`
- <a id="nuc-numeros-12"></a>**En contratos.** Un decimal se interpreta como su coeficiente entero, de modo que la mayoría de sus operaciones quedan en aritmética lineal entera. `nuc-numeros-12`

## <a id="nuc-memoria"></a>Memoria

<a id="nuc-memoria-1"></a>Todos los lenguajes comparten un único modelo de memoria. Zea, Talud y Relevo lo exponen con préstamos explícitos; Solsticio, Voluta y Amate solo tienen valores inmutables y su compartición se resuelve al compilar. `nuc-memoria-1`

- <a id="nuc-memoria-2"></a>Cada valor tiene un único dueño. Asignar o pasar por valor mueve, salvo en los escalares, que se copian. `nuc-memoria-2`
- <a id="nuc-memoria-3"></a>Un préstamo compartido permite leer; uno exclusivo permite modificar y excluye cualquier otro préstamo simultáneo. Ningún préstamo sobrevive a su dueño. `nuc-memoria-3`
- <a id="nuc-memoria-4"></a>En una firma, todo préstamo que aparece en el resultado declara de qué parámetro proviene. `nuc-memoria-4`
- <a id="nuc-memoria-5"></a>La memoria dinámica existe solo a través de un efecto declarado. La liberación ocurre al final del ámbito del dueño y es explícita en la representación intermedia. `nuc-memoria-5`
- <a id="nuc-memoria-6"></a>Los dueños múltiples se obtienen por conteo de referencias. Un tipo con conteo de referencias no puede contenerse a sí mismo de forma transitiva; los enlaces de vuelta son débiles. `nuc-memoria-6`
- <a id="nuc-memoria-7"></a>Un valor puede moverse a otra tarea si su tipo es transferible (*Send*) y compartirse por préstamo inmutable si es compartible (*Sync*). Los préstamos exclusivos nunca se comparten. El compilador determina ambas propiedades a partir de los campos y el verificador las comprueba. `nuc-memoria-7`
- <a id="nuc-memoria-8"></a>No hay variables globales mutables: las constantes se inicializan en compilación y todo estado mutable se pasa explícitamente o vive detrás de un efecto. `nuc-memoria-8`

### <a id="nuc-prestamos"></a>Préstamos

<a id="nuc-memoria-9"></a>La comprobación de préstamos es un análisis de flujo de datos sobre el grafo de control, en tiempo polinómico, que el verificador repite. `nuc-memoria-9`

- <a id="nuc-memoria-10"></a>**Lugares.** Un préstamo se toma de un lugar: una variable, un campo de un lugar o un elemento de un lugar. Dos préstamos están en conflicto si sus lugares se solapan y al menos uno es exclusivo. `nuc-memoria-10`
- <a id="nuc-memoria-11"></a>**Campos disjuntos.** Campos distintos de un registro son lugares disjuntos. Dos elementos de un arreglo no se consideran disjuntos por su índice; se separan con una operación que divide una vista en dos. `nuc-memoria-11`
- <a id="nuc-memoria-12"></a>**Vida.** Un préstamo vive desde que se toma hasta su último uso en cualquier camino del grafo de control. Un préstamo guardado en un lugar vive mientras ese lugar pueda usarse. `nuc-memoria-12`
- <a id="nuc-memoria-13"></a>**Re-préstamo.** De un préstamo exclusivo puede tomarse otro, compartido o exclusivo; mientras vive, el original no puede usarse. `nuc-memoria-13`
- <a id="nuc-memoria-14"></a>**Movimiento parcial.** Mover un campo deja el registro parcialmente movido hasta que el campo se reasigna. Un registro con destructor propio no admite movimiento parcial. `nuc-memoria-14`
- <a id="nuc-memoria-15"></a>**Bucles.** Un préstamo tomado en una iteración no sobrevive a ella salvo que se guarde en el estado del bucle. El análisis trata cada bucle como si su cuerpo se ejecutara dos veces seguidas. `nuc-memoria-15`
- <a id="nuc-memoria-16"></a>**Clausuras.** Cada captura declara si toma un préstamo compartido, uno exclusivo o mueve el valor. `nuc-memoria-16`

## <a id="nuc-modulos"></a>Módulos

- <a id="nuc-modulos-1"></a>Un módulo es un conjunto de archivos que comparten espacio de nombres; un paquete es un conjunto de módulos con un manifiesto. `nuc-modulos-1`
- <a id="nuc-modulos-2"></a>Los imports nombran cada símbolo, sin comodines, y pueden renombrarlo. Dos imports que introducen el mismo nombre, o un import con el nombre de una declaración del módulo, son un error. `nuc-modulos-2`
- <a id="nuc-modulos-3"></a>Un archivo puede condicionarse a un destino y convertirse en [variante por destino](20-destinos.md#dst-variantes). `nuc-modulos-3`

| Visibilidad                              | Visible en                       | Parte de la interfaz pública                                        |
|------------------------------------------|----------------------------------|---------------------------------------------------------------------|
| <a id="nuc-modulos-4"></a>Privada (predeterminada) `nuc-modulos-4` | El módulo                        | No                                                                  |
| <a id="nuc-modulos-5"></a>De paquete `nuc-modulos-5`               | Todo el paquete                  | No                                                                  |
| <a id="nuc-modulos-6"></a>Pública `nuc-modulos-6`                  | Cualquier paquete que la importe | Sí: entra en la identidad de la interfaz y en el cálculo de versión |

<a id="nuc-modulos-7"></a>Un módulo puede reexportar un símbolo importado; la reexportación es una declaración pública más. `nuc-modulos-7`

## <a id="nuc-archivos"></a>Clases de archivo

<a id="nuc-archivos-1"></a>El código de un módulo se reparte en tres clases de archivo, que se distinguen sin ambigüedad: `nuc-archivos-1`

| Clase                         | Contiene                                                                    | Llega a                                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| <a id="nuc-archivos-2"></a>Ejecutable `nuc-archivos-2`   | Las declaraciones de código y sus contratos, incluidas las citas a lemas.   | La parte de código del módulo y el binario.                                             |
| <a id="nuc-archivos-3"></a>Demostración `nuc-archivos-3` | Funciones fantasma, lemas, extensiones fantasma y actualizaciones fantasma. | La parte fantasma del módulo y la evidencia de la atestación. El backend la borra.      |
| <a id="nuc-archivos-4"></a>Pruebas `nuc-archivos-4`      | Pruebas y lo que solo usan las pruebas.                                     | Un módulo de pruebas que solo se compila para ejecutar pruebas. Nunca entra al binario. |

- <a id="nuc-archivos-5"></a>**Ubicación.** Cada declaración va en su clase de archivo; cualquier otra ubicación es un error de compilación. `nuc-archivos-5`
- <a id="nuc-archivos-6"></a>**Visibilidad.** Los contratos de un archivo ejecutable pueden nombrar funciones fantasma y lemas; el código ejecutable no. Los archivos de demostración y de pruebas ven todo el módulo. Nada de un archivo de pruebas puede importarse desde un archivo ejecutable o de demostración. `nuc-archivos-6`
- <a id="nuc-archivos-7"></a>**Verificación.** Las pruebas son código ejecutable y pasan por el verificador como cualquier otro. Dentro de una prueba existe una comprobación propia que se evalúa al ejecutarla y que no es una VC. `nuc-archivos-7`
- <a id="nuc-archivos-8"></a>**Identidad.** El código, la parte fantasma y las pruebas tienen identidades separadas, y la del binario depende solo del código. El diff de significado agrupa los cambios en código, demostraciones y pruebas. `nuc-archivos-8`
- <a id="nuc-archivos-9"></a>**Mutación.** Solo se muta el código ejecutable. Un mutante muere por un contrato, por una prueba de propiedades o por una prueba. `nuc-archivos-9`
- <a id="nuc-archivos-10"></a>**Ejecución de pruebas.** Se ejecutan las pruebas declaradas, pruebas de propiedades generadas a partir de las precondiciones de cada función pública y los ejemplos de la documentación. Con el motor simulado, la planificación, el tiempo y los fallos se reproducen a partir de una semilla. `nuc-archivos-10`

## <a id="nuc-documentacion"></a>Documentación en el código

- <a id="nuc-documentacion-1"></a>Los comentarios de documentación se adjuntan a una declaración y se escriben en CommonMark 0.31.2. Son de línea, como todo comentario. `nuc-documentacion-1`
- <a id="nuc-documentacion-2"></a>Forman parte de la interfaz pública del módulo, pero no de su identidad: un cambio solo de documentación no cambia la identidad del módulo y es un incremento de parche. `nuc-documentacion-2`
- <a id="nuc-documentacion-3"></a>Glosa reporta los cambios de documentación de la interfaz pública en una categoría propia, separada de los cambios de significado. `nuc-documentacion-3`
- <a id="nuc-documentacion-4"></a>Los ejemplos de código de la documentación son código de pruebas: se compilan, se verifican y se ejecutan con las pruebas del módulo, así que un ejemplo que deja de ser correcto rechaza el módulo. `nuc-documentacion-4`
- <a id="nuc-documentacion-5"></a>Toda declaración pública de un paquete publicado en el registro DEBE tener documentación. `nuc-documentacion-5`
- <a id="nuc-documentacion-6"></a>La documentación no es fuente de garantías: lo que un comentario afirma sin expresarlo en un contrato no se verifica. `nuc-documentacion-6`

## <a id="nuc-contratos"></a>Contratos

<a id="nuc-contratos-1"></a>Un contrato es una afirmación que el verificador DEBE ver resuelta con evidencia. Sus clases son las mismas en los seis lenguajes: `nuc-contratos-1`

| Clase                                   | Significado                                                                                                                                                   |
|-----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <a id="nuc-contratos-2"></a>Precondición `nuc-contratos-2`          | DEBE cumplirse al llamar; se verifica en cada punto de llamada.                                                                                               |
| <a id="nuc-contratos-3"></a>Postcondición `nuc-contratos-3`         | Se cumple al retornar. Puede referirse al resultado, a cada variante de un resultado con error y al valor de una expresión al entrar.                         |
| <a id="nuc-contratos-4"></a>Invariante `nuc-contratos-4`            | En bucles, vale al inicio de cada iteración; en registros, clases y actores, para todo valor observable desde fuera.                                          |
| <a id="nuc-contratos-5"></a>Medida de terminación `nuc-contratos-5` | Decrece estrictamente en cada iteración o llamada recursiva, en un orden bien fundado.                                                                        |
| <a id="nuc-contratos-6"></a>Afirmación intermedia `nuc-contratos-6` | Crea una VC en un punto del código.                                                                                                                           |
| <a id="nuc-contratos-7"></a>Cita de lema `nuc-contratos-7`          | Aplica uno o más lemas, con sus argumentos, para demostrar la cláusula a la que acompaña. Es la única forma en que el código ejecutable usa una demostración. |

<a id="nuc-contratos-8"></a>Las expresiones de contrato solo llaman funciones puras y totales. La lógica admitida es aritmética lineal entera, vectores de bits, arreglos, tipos algebraicos y cuantificadores acotados sobre rangos o colecciones finitas. Dentro de un contrato los enteros son matemáticos. Qué decide el solucionador y qué ocurre con el resto está en [Límites de la computación](#nuc-limites). `nuc-contratos-8`

## <a id="nuc-fantasma"></a>Código fantasma

<a id="nuc-fantasma-1"></a>El código fantasma aporta lo que el solucionador no hace solo: inducción, aritmética no lineal e instanciación de enunciados generales. Existe solo para la verificación, vive en los archivos de demostración, el verificador lo comprueba como el resto y el backend lo borra, así que no amplía la TCB. `nuc-fantasma-1`

| Elemento                                | Uso                                                                                                                                                                                   |
|-----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <a id="nuc-fantasma-2"></a>Función fantasma `nuc-fantasma-2`       | Define un concepto matemático para usarlo en contratos. Pura y total; si es recursiva, lleva medida de terminación.                                                                   |
| <a id="nuc-fantasma-3"></a>Lema `nuc-fantasma-3`                   | Un teorema con su demostración: sus precondiciones son las hipótesis y sus postcondiciones, la conclusión.                                                                            |
| <a id="nuc-fantasma-4"></a>Extensión fantasma `nuc-fantasma-4`     | Añade a un tipo, clase, trait o actor campos fantasma con un estado abstracto, o funciones de modelo. En un trait, la función de modelo es abstracta y cada implementación la define. |
| <a id="nuc-fantasma-5"></a>Actualización fantasma `nuc-fantasma-5` | Fija el valor de los campos fantasma de un tipo cuando una función termina, a partir de sus parámetros, su resultado y los valores de entrada.                                        |
| <a id="nuc-fantasma-6"></a>Tipos matemáticos `nuc-fantasma-6`      | Enteros sin cota, naturales, reales, secuencias, conjuntos y mapas. Solo existen en código fantasma y en contratos.                                                                   |

### <a id="nuc-fantasma-reglas"></a>Reglas

- <a id="nuc-fantasma-7"></a>**Borrado.** Ningún valor fantasma fluye hacia código ejecutable, y el código fantasma no tiene efectos ni modifica estado ejecutable. Borrarlo no cambia el comportamiento del programa. `nuc-fantasma-7`
- <a id="nuc-fantasma-8"></a>**Terminación.** Toda función fantasma, lema y bucle fantasma termina, con medida de terminación si es recursivo o itera. `nuc-fantasma-8`
- <a id="nuc-fantasma-9"></a>**Dependencias.** El grafo de demostraciones (qué lemas y qué contratos usa cada demostración) es acíclico. Una demostración usa el contrato de otra función, nunca su demostración. Solo se admiten ciclos entre lemas y funciones fantasma mutuamente recursivos con una medida común. `nuc-fantasma-9`
- <a id="nuc-fantasma-10"></a>**Desarrollo.** En cada VC, cada llamada a una función fantasma se desarrolla una sola vez; lo que requiera más se expresa con lemas. `nuc-fantasma-10`
- <a id="nuc-fantasma-11"></a>**Instanciación explícita.** Un enunciado general se escribe como lema con parámetros y se aplica con una cita y los valores concretos. `nuc-fantasma-11`
- <a id="nuc-fantasma-12"></a>**Evidencia.** Toda VC de código fantasma se resuelve con un certificado; no admite comprobación en ejecución. Un lema se demuestra una vez y quien lo usa lo referencia por su identidad. `nuc-fantasma-12`
- <a id="nuc-fantasma-13"></a>**Mutación.** El código fantasma no se muta, y R5 no se aplica a los lemas. `nuc-fantasma-13`

## <a id="nuc-traits"></a>Traits

<a id="nuc-traits-1"></a>Un trait declara funciones con contratos. `nuc-traits-1`

- <a id="nuc-traits-2"></a>**Miembros.** Funciones, con o sin comportamiento por defecto; tipos asociados, que cada implementación fija; y constantes asociadas. `nuc-traits-2`
- <a id="nuc-traits-3"></a>**Supertraits.** Un trait puede exigir que todo tipo que lo implemente implemente otros. `nuc-traits-3`
- <a id="nuc-traits-4"></a>**Proyecciones explícitas.** Un tipo asociado se nombra siempre; nunca se deduce. `nuc-traits-4`
- <a id="nuc-traits-5"></a>**Refinamiento.** Una implementación puede debilitar precondiciones y fortalecer postcondiciones, nunca lo contrario, y no puede declarar más efectos que el trait. `nuc-traits-5`
- <a id="nuc-traits-6"></a>**Coherencia.** En todo el programa existe como máximo una implementación para cada par trait–tipo, escrita en el paquete del trait o en el que define el tipo. Una implementación para todos los tipos que cumplan un límite solo puede escribirse en el paquete del trait, y como máximo una por trait. `nuc-traits-6`
- <a id="nuc-traits-7"></a>**Resolución.** Con instanciación explícita y coherencia, resolver qué implementación usa una llamada es una búsqueda finita que nunca retrocede. `nuc-traits-7`
- <a id="nuc-traits-8"></a>**Despacho dinámico.** Un trait puede usarse como objeto si ninguna de sus funciones es genérica en tipos, ninguna recibe o devuelve el propio tipo por valor salvo como receptor, y no tiene constantes asociadas. Sus tipos asociados se fijan en el tipo del objeto. `nuc-traits-8`

### <a id="nuc-derivacion"></a>Derivación

<a id="nuc-traits-9"></a>Un tipo puede pedir la implementación de ciertos traits a partir de su estructura. La genera el compilador con una regla fija, sin código del usuario, y queda marcada como derivada. `nuc-traits-9`

| Trait                                  | Regla                                                                                                                          | Leyes que se demuestran                              |
|----------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------|
| <a id="nuc-traits-10"></a>Igualdad `nuc-traits-10`               | Registros: iguales si todos sus campos lo son. Sumas: misma variante y contenidos iguales.                                     | Reflexiva, simétrica, transitiva                     |
| <a id="nuc-traits-11"></a>Orden `nuc-traits-11`                  | Lexicográfico en el orden de declaración de campos y de variantes.                                                             | Orden total, coherente con la igualdad               |
| <a id="nuc-traits-12"></a>Hash `nuc-traits-12`                   | Combina los hashes de los campos en orden de declaración con un combinador fijo; en sumas, primero la variante.                | Valores iguales tienen el mismo hash                 |
| <a id="nuc-traits-13"></a>Representación textual `nuc-traits-13` | El nombre del tipo o de la variante seguido de sus campos en orden de declaración.                                             | Determinista                                         |
| <a id="nuc-traits-14"></a>Codificación `nuc-traits-14`           | Al modelo de datos de CBOR: un registro es un mapa con una clave por campo; una suma, un mapa con una sola clave, la variante. | —                                                    |
| <a id="nuc-traits-15"></a>Decodificación `nuc-traits-15`         | La inversa exacta; una clave que falta o sobra, o un tipo distinto, es un error.                                               | Decodificar lo codificado devuelve el valor original |

- <a id="nuc-traits-16"></a>Solo se puede derivar un trait si todos los campos lo implementan. La lista de traits derivados es parte de la interfaz del tipo. `nuc-traits-16`
- <a id="nuc-traits-17"></a>El verificador demuestra las leyes de cada implementación generada. La mutación no las muta. `nuc-traits-17`
- <a id="nuc-traits-18"></a>Las propiedades transferible y compartible no se derivan: el compilador siempre las determina. `nuc-traits-18`
- <a id="nuc-traits-19"></a>La representación textual de un valor conserva su procedencia: la de un dato secreto es secreta. `nuc-traits-19`

## <a id="nuc-efectos"></a>Efectos

<a id="nuc-efectos-1"></a>Toda función declara los efectos que puede producir; sin efectos declarados es pura y total. Los efectos de una función contienen los de todo lo que llama. Una función de orden superior declara variables de efecto, que se instancian explícitamente en cada llamada. Una biblioteca puede declarar subefectos de otro efecto. `nuc-efectos-1`

| Efecto primitivo                       | Significado                                                                                         |
|----------------------------------------|-----------------------------------------------------------------------------------------------------|
| <a id="nuc-efectos-2"></a>Memoria dinámica `nuc-efectos-2`       | Reserva y libera memoria. Lo provee un proveedor.                                                   |
| <a id="nuc-efectos-3"></a>Memoria externa `nuc-efectos-3`        | Lee o escribe memoria que no pertenece al programa.                                                 |
| <a id="nuc-efectos-4"></a>Intrínseco del destino `nuc-efectos-4` | Invoca una operación de la especificación del destino. Es la raíz de todo efecto sobre el exterior. |
| <a id="nuc-efectos-5"></a>No terminación `nuc-efectos-5`         | La función puede no terminar.                                                                       |

<a id="nuc-efectos-6"></a>Sobre ellos, la plataforma define los efectos de tareas, reloj monótono, telemetría, consulta de extensiones del procesador, llamada a código nativo aislado, carga de plugins, mensajes entre actores, celdas mutables y acceso al hardware en freestanding. La biblioteca estándar declara los suyos como subefectos de los intrínsecos. `nuc-efectos-6`

## <a id="nuc-procedencia"></a>Procedencia

- <a id="nuc-procedencia-1"></a>Cualquier tipo puede llevar una etiqueta que dice de dónde viene el valor y qué puede hacer. Tipos con distinta etiqueta no son intercambiables. `nuc-procedencia-1`
- <a id="nuc-procedencia-2"></a>La única conversión entre etiquetas es una función declarada como justificación de esa conversión, cuyo contrato demuestra lo que valida. `nuc-procedencia-2`
- <a id="nuc-procedencia-3"></a>Una etiqueta puede refinar a otra y usarse donde se espera la más general. `nuc-procedencia-3`
- <a id="nuc-procedencia-4"></a>La plataforma define tres etiquetas: *external* para todo lo que entra por una frontera, *secret* para datos sensibles y *peer* para lo que llega de un par verificado. `nuc-procedencia-4`

### <a id="nuc-secretos"></a>Datos secretos y tiempo constante

<a id="nuc-procedencia-5"></a>Un dato secreto NO DEBE filtrarse por el tiempo de ejecución, por los accesos a memoria ni por la ejecución especulativa. La plataforma lo garantiza con una disciplina de flujo de información que el verificador comprueba y con obligaciones del backend. Los canales físicos (consumo, emisiones, inyección de fallos) quedan fuera del modelo. `nuc-procedencia-5`

- <a id="nuc-procedencia-6"></a>**Propagación.** El resultado de una operación con algún operando secreto es secreto, incluida la variante de un tipo suma. `nuc-procedencia-6`
- <a id="nuc-procedencia-7"></a>**Prohibido.** Un dato secreto no puede determinar una condición o una variante inspeccionada, un índice, una dirección, un tamaño, la cota o la medida de un bucle, una salida anticipada, un operando de una operación que el destino no declara de tiempo constante, el destino de una llamada indirecta ni ninguna salida observable. `nuc-procedencia-7`
- <a id="nuc-procedencia-8"></a>**Admitido.** Las operaciones de tiempo constante del destino, las comparaciones, la selección sin bifurcación (que evalúa ambos lados) y la comparación de secuencias que recorre siempre la longitud completa. `nuc-procedencia-8`
- <a id="nuc-procedencia-9"></a>**Desclasificación.** Solo en una función de justificación, y cada una figura en el diff de significado y en la atestación. `nuc-procedencia-9`
- <a id="nuc-procedencia-10"></a>**Borrado.** Cuando un dato secreto se destruye, el backend sobrescribe su memoria con una operación que ninguna optimización elimina, y limpia los registros y la pila que lo contuvieron. `nuc-procedencia-10`
- <a id="nuc-procedencia-11"></a>**Memoria del sistema.** Si el destino ofrece excluir memoria del intercambio a disco y de los volcados, se usa para los secretos; si no, la exposición figura en el inventario de confianza. `nuc-procedencia-11`

### <a id="nuc-secretos-especulacion"></a>Ejecución especulativa

<a id="nuc-procedencia-12"></a>El verificador analiza el programa con una semántica especulativa: cualquier rama puede predecirse mal durante una ventana acotada, y los accesos de esa ventana dejan huella. Las protecciones se aplican solo donde ese análisis encuentra un riesgo: `nuc-procedencia-12`

| Riesgo                                                                                                                                                                  | Protección                                                                                         |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| <a id="nuc-procedencia-13"></a>Omisión especulativa de una comprobación de límites (CVE-2017-5753), con índice externo o secreto, en un espacio de direcciones con datos secretos `nuc-procedencia-13` | Enmascarado del índice con la condición de la comprobación de límites; barrera donde no es posible |
| <a id="nuc-procedencia-14"></a>Inyección en el destino de saltos indirectos (CVE-2017-5715), en funciones que manejan secretos `nuc-procedencia-14`                                                    | La protección de saltos indirectos del destino                                                     |
| <a id="nuc-procedencia-15"></a>Desvío de la predicción de retornos (CVE-2018-15572), en esas mismas funciones `nuc-procedencia-15`                                                                     | La protección de retornos del destino                                                              |
| <a id="nuc-procedencia-16"></a>Omisión especulativa de un almacenamiento (CVE-2018-3639), sobre datos secretos `nuc-procedencia-16`                                                                    | Barrera de especulación                                                                            |

<a id="nuc-procedencia-17"></a>Un riesgo para el que el destino no tiene protección no bloquea la compilación: figura en el inventario de confianza como especulación no mitigada. `nuc-procedencia-17`

## <a id="nuc-fronteras"></a>Fronteras asíncronas

<a id="nuc-fronteras-1"></a>Una frontera asíncrona conecta el programa con algo que no controla ni verifica, mediante operaciones que van y vuelven: otro proceso, otra máquina, un almacenamiento, un dispositivo con colas, un acelerador, código nativo aislado o un servicio externo. El otro lado puede fallar por separado. Toda frontera declara su **modelo de fallos**, y el lenguaje exige manejar exactamente los fallos declarados. `nuc-fronteras-1`

<a id="nuc-fronteras-2"></a>El modelo usa la taxonomía estándar de fallos de sistemas confiables (Avižienis, Laprie, Randell y Landwehr, 2004) y las abstracciones de enlace y de detección de fallos de la programación distribuida fiable (Cachin, Guerraoui y Rodrigues, 2011; Chandra y Toueg, 1996). Los fallos arbitrarios (bizantinos) no se modelan: una frontera cuyo otro lado puede mentir se trata como no confiable y todo lo que llega es *external*. `nuc-fronteras-2`

| Fallo                               | Significado                                                                | Sin él, la frontera garantiza                                                        |
|-------------------------------------|----------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| <a id="nuc-fronteras-3"></a>Pérdida `nuc-fronteras-3`           | Un mensaje enviado puede no entregarse nunca.                              | Ningún mensaje se descarta en silencio: si no se entrega, el emisor recibe un error. |
| <a id="nuc-fronteras-4"></a>Duplicación `nuc-fronteras-4`       | Un mensaje puede entregarse más de una vez.                                | Cada mensaje se entrega como máximo una vez.                                         |
| <a id="nuc-fronteras-5"></a>Reordenamiento `nuc-fronteras-5`    | Los mensajes pueden entregarse en otro orden.                              | Los mensajes entregados conservan el orden de envío.                                 |
| <a id="nuc-fronteras-6"></a>Retraso `nuc-fronteras-6`           | La entrega no tiene cota de tiempo.                                        | La entrega tiene la cota que declara la frontera.                                    |
| <a id="nuc-fronteras-7"></a>Caída `nuc-fronteras-7`             | El otro lado puede dejar de responder o reiniciarse.                       | El otro lado responde mientras la frontera esté abierta.                             |
| <a id="nuc-fronteras-8"></a>Escritura parcial `nuc-fronteras-8` | Una escritura sin confirmar puede quedar a medias tras una caída.          | Toda escritura queda completa o no queda.                                            |
| <a id="nuc-fronteras-9"></a>Corrupción `nuc-fronteras-9`        | Los datos pueden alterarse en el camino; la alteración siempre se detecta. | Los datos llegan sin alterar.                                                        |

- <a id="nuc-fronteras-10"></a>En toda frontera, un mensaje entregado fue enviado: nada se fabrica, y una alteración detectada se entrega como error. `nuc-fronteras-10`
- <a id="nuc-fronteras-11"></a>El tipo de error de una frontera solo tiene las variantes de sus fallos declarados: plazo vencido, frontera cerrada, datos corruptos y resultado desconocido (la petición puede haberse ejecutado o no). `nuc-fronteras-11`
- <a id="nuc-fronteras-12"></a>Toda espera sobre una frontera con retraso, pérdida o caída lleva plazo. `nuc-fronteras-12`
- <a id="nuc-fronteras-13"></a>Lo que llega es *external*, salvo de un par verificado, donde es *peer*. `nuc-fronteras-13`
- <a id="nuc-fronteras-14"></a>Lo que cruza una frontera que sale del proceso es codificable y viaja en CBOR determinista (RFC 8949, sección 4.2), con su esquema en CDDL (RFC 8610) e identificado por la interfaz de la frontera. `nuc-fronteras-14`
- <a id="nuc-fronteras-15"></a>Cada frontera declara el efecto que exigen sus operaciones. `nuc-fronteras-15`

### <a id="nuc-fronteras-composicion"></a>Composición e idempotencia

- <a id="nuc-fronteras-16"></a>**Sesión.** Numera los mensajes y descarta duplicados y desordenados: sobre un enlace con pérdidas equitativas construye un enlace FIFO, con posibles huecos. `nuc-fronteras-16`
- <a id="nuc-fronteras-17"></a>**Reintento.** Reenvía hasta recibir respuesta o vencer el plazo (enlace insistente). Solo se admite hacia operaciones idempotentes; con sesión, da un enlace perfecto FIFO y procesamiento efectivamente único. `nuc-fronteras-17`
- <a id="nuc-fronteras-18"></a>**Integridad.** Añade un código de integridad: convierte una alteración no detectable del medio en corrupción detectada. `nuc-fronteras-18`
- <a id="nuc-fronteras-19"></a>**Idempotencia.** Una función o manejador declarado idempotente genera la VC de que aplicarlo dos veces con los mismos argumentos deja el mismo estado y la misma respuesta que aplicarlo una. Se demuestra como cualquier contrato. `nuc-fronteras-19`

### <a id="nuc-fronteras-instancias"></a>Instancias

| Frontera                                                                     | Fallos                                                      |
|------------------------------------------------------------------------------|-------------------------------------------------------------|
| <a id="nuc-fronteras-20"></a>Canal dentro del proceso, buzón de un actor local `nuc-fronteras-20`         | Ninguno; enviar a un canal lleno espera                     |
| <a id="nuc-fronteras-21"></a>Código nativo aislado, biblioteca exportada como servicio `nuc-fronteras-21` | Caída, retraso, corrupción                                  |
| <a id="nuc-fronteras-22"></a>Otro proceso de la misma máquina `nuc-fronteras-22`                          | Caída, retraso                                              |
| <a id="nuc-fronteras-23"></a>Almacenamiento `nuc-fronteras-23`                                            | Escritura parcial, reordenamiento antes de confirmar, caída |
| <a id="nuc-fronteras-24"></a>Dispositivo con colas de peticiones `nuc-fronteras-24`                       | Retraso, reordenamiento de finalizaciones                   |
| <a id="nuc-fronteras-25"></a>Acelerador o coprocesador `nuc-fronteras-25`                                 | Retraso, caída del trabajo                                  |
| <a id="nuc-fronteras-26"></a>Red `nuc-fronteras-26`                                                       | Todos                                                       |
| <a id="nuc-fronteras-27"></a>Par externo `nuc-fronteras-27`                                               | Los de su transporte                                        |

<a id="nuc-fronteras-28"></a>La memoria compartida, los atómicos y los registros de hardware mapeados en memoria no son fronteras asíncronas: siguen el [modelo de memoria](10-stela.md#stx-memoria). `nuc-fronteras-28`

### <a id="nuc-fronteras-almacenamiento"></a>Almacenamiento

<a id="nuc-fronteras-29"></a>Una frontera de almacenamiento tiene una operación de confirmación y un modelo fantasma con lo confirmado y lo pendiente. Tras una caída, el contenido es lo confirmado más cualquier subconjunto de lo pendiente, con escrituras parciales si el modelo las declara. Una función fantasma enumera esos estados, así que un programa puede demostrar que sus datos quedan consistentes después de cualquier caída. `nuc-fronteras-29`

## <a id="nuc-comptime"></a>Evaluación en compilación

- <a id="nuc-comptime-1"></a>El código puede evaluarse en compilación en un evaluador sin efectos externos, salvo la lectura de archivos del propio paquete. Voluta lo hace con macros; los demás, con evaluación de expresiones. No hay transformación textual. `nuc-comptime-1`
- <a id="nuc-comptime-2"></a>Lo que se evalúa en compilación es total, sin el efecto de no terminación, y corre con un presupuesto determinista de pasos. Agotarlo es un error de compilación, igual en cualquier máquina. `nuc-comptime-2`
- <a id="nuc-comptime-3"></a>El resultado entra en la representación intermedia y se verifica como el resto. `nuc-comptime-3`

## <a id="nuc-limites"></a>Límites de la computación

<a id="nuc-limites-1"></a>La plataforma no decide propiedades: comprueba evidencia. El programa aporta medidas de terminación, contratos, invariantes y lemas; el solucionador busca pruebas dentro de un presupuesto; el verificador solo comprueba certificados, lo que siempre termina. Lo que no se demuestra se comprueba en ejecución cuando es posible, o se rechaza. La verificación es correcta (nunca acepta algo falso) e incompleta (puede rechazar algo verdadero). `nuc-limites-1`

| Límite                                                                                  | Regla                                                                                                                                                                                                                          |
|-----------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <a id="nuc-limites-2"></a>Terminación de programas (indecidible) `nuc-limites-2`                                  | Se demuestra con una medida en un orden bien fundado. Lo que no la tiene declara el efecto de no terminación; con él la familia es Turing-completa, y sin él toda función termina.                                             |
| <a id="nuc-limites-3"></a>Propiedades semánticas (teorema de Rice) `nuc-limites-3`                                | Nada decide equivalencia ni propiedades semánticas por sí solo. La identidad, el formateador y el diff de significado comparan formas canónicas y declaraciones. Un mutante solo se descarta como equivalente con certificado. |
| <a id="nuc-limites-4"></a>Incompletitud de la aritmética `nuc-limites-4`                                          | El verificador es incompleto y lo declara. Su consistencia no se demuestra con él mismo sino en un asistente de pruebas externo, y la del binario se ancla con doble compilación diversa.                                      |
| <a id="nuc-limites-5"></a>Aritmética entera no lineal (indecidible) `nuc-limites-5`                               | El solucionador la trata como funciones no interpretadas; sus propiedades se aportan con lemas.                                                                                                                                |
| <a id="nuc-limites-6"></a>Complejidad de la decisión (NP y superiores) `nuc-limites-6`                            | Toda búsqueda de pruebas corre con un presupuesto determinista. El resto de las fases es polinómico.                                                                                                                           |
| <a id="nuc-limites-7"></a>Entrega exactamente una vez (dos generales) `nuc-limites-7`                             | Imposible sobre una frontera con pérdida. Se obtiene procesamiento efectivamente único con reintento hacia un receptor idempotente.                                                                                            |
| <a id="nuc-limites-8"></a>Consenso con fallos en un sistema asíncrono (Fischer, Lynch y Paterson) `nuc-limites-8` | La plataforma no ofrece consenso; una biblioteca que lo implemente declara las suposiciones de tiempo que necesita.                                                                                                            |
| <a id="nuc-limites-9"></a>Consistencia y disponibilidad durante una partición (Gilbert y Lynch) `nuc-limites-9`   | No se pueden garantizar ambas. Cada operación sobre una frontera con pérdida o caída elige en su tipo entre un resultado desconocido y un valor local declarado como posiblemente desactualizado.                              |
| <a id="nuc-limites-10"></a>Detección de fallos (Chandra y Toueg) `nuc-limites-10`                                  | Un nodo caído no se distingue de uno lento: la plataforma ofrece un detector de fallos eventualmente perfecto, basado en plazos, y una caída remota es siempre una sospecha.                                                   |

### <a id="nuc-limites-terminacion"></a>Terminación y medidas

- <a id="nuc-limites-11"></a>**Orden bien fundado.** Una medida es un entero sin signo de ancho fijo, un natural, un entero matemático con la VC de que no es negativo, el tamaño estructural de un valor algebraico o una tupla de medidas en orden lexicográfico. `nuc-limites-11`
- <a id="nuc-limites-12"></a>**Recursión mutua.** Las funciones de un mismo ciclo de llamadas declaran medidas del mismo tipo, y cada llamada dentro del ciclo la hace decrecer. `nuc-limites-12`
- <a id="nuc-limites-13"></a>**Ejecución indefinida.** Un programa que debe correr indefinidamente declara el efecto de no terminación. Las demás garantías se mantienen. `nuc-limites-13`

### <a id="nuc-limites-compilacion"></a>Terminación de la compilación

- <a id="nuc-limites-14"></a>**Análisis sintáctico** en tiempo lineal, por los principios de sintaxis. `nuc-limites-14`
- <a id="nuc-limites-15"></a>**Tipos, efectos, préstamos y procedencia**: un recorrido con reglas locales, en tiempo polinómico, porque no hay inferencia. `nuc-limites-15`
- <a id="nuc-limites-16"></a>**Instanciación.** La recursión polimórfica se rechaza, así que la monomorfización produce un conjunto finito de instancias. `nuc-limites-16`
- <a id="nuc-limites-17"></a>**Evaluación en compilación**: total y con presupuesto. `nuc-limites-17`
- <a id="nuc-limites-18"></a>**Amate**: ninguna regla recursiva crea valores nuevos, así que el punto fijo existe y se alcanza. `nuc-limites-18`

### <a id="nuc-limites-solucionador"></a>Veredictos del solucionador

- <a id="nuc-limites-19"></a>**Tres resultados.** Cada VC queda demostrada (con certificado), refutada (con contraejemplo) o desconocida (sin respuesta dentro del presupuesto). `nuc-limites-19`
- <a id="nuc-limites-20"></a>**Presupuesto determinista.** Se mide en pasos del solucionador, no en tiempo. La misma VC con el mismo presupuesto y la misma versión da el mismo resultado en cualquier máquina, y el presupuesto queda en la atestación. `nuc-limites-20`
- <a id="nuc-limites-21"></a>**Fragmento decidible.** Aritmética lineal entera, vectores de bits, arreglos, tipos algebraicos y sus combinaciones sin cuantificadores. Un cuantificador acotado en una hipótesis se instancia solo con los términos que ya aparecen en la VC; fuera de ese fragmento, la instanciación se escribe con un lema. `nuc-limites-21`
- <a id="nuc-limites-22"></a>**VC desconocida.** En código ejecutable, se compila como comprobación en ejecución si todos sus términos son ejecutables y la política del paquete lo admite; si menciona código fantasma o tipos matemáticos, el programa se rechaza. En código fantasma, siempre se rechaza. `nuc-limites-22`

### <a id="nuc-limites-consistencia"></a>Consistencia de las suposiciones

- <a id="nuc-limites-23"></a>**Razonamiento circular.** Lo impide la regla de dependencias del [código fantasma](#nuc-fantasma-reglas). `nuc-limites-23`
- <a id="nuc-limites-24"></a>**Vacuidad.** Por cada función, invariante y especificación de destino, la cadena de herramientas intenta demostrar falso a partir de sus suposiciones, dentro del presupuesto del solucionador, y si lo consigue rechaza el programa. Es un diagnóstico de calidad, no una garantía: unas precondiciones contradictorias no pueden demostrarse en ningún punto de llamada y una invariante contradictoria no puede establecerse al construir el valor, así que no hacen aceptar nada falso. Solo los axiomas de una especificación de destino podrían hacerlo; por eso las especificaciones de destino son parte de la TCB y su consistencia se comprueba al admitirlas ([Gobierno de las especificaciones](19-rumbo.md#dst-gobierno)). El verificador no repite esta búsqueda. `nuc-limites-24`
- <a id="nuc-limites-25"></a>**Contratos totales.** Como los contratos solo llaman funciones puras y totales, ninguna definición introduce una ecuación contradictoria. `nuc-limites-25`

### <a id="nuc-limites-concurrencia"></a>Concurrencia

<a id="nuc-limites-26"></a>La ausencia de interbloqueos es indecidible en general. La plataforma la garantiza entre actores locales de Relevo, cuyo grafo de esperas DEBE ser acíclico; las esperas sobre actores remotos y sobre cualquier frontera quedan acotadas por su plazo obligatorio. La concurrencia estructurada garantiza que toda tarea termina dentro de su ámbito. `nuc-limites-26`

---

← [Familia de lenguajes](01-familia.md) · [Índice](README.md) · [Zea](03-zea.md) →
