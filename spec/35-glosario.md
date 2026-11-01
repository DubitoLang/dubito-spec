---
title: "Glosario"
order: 35
---
*Referencia*

# Glosario

**Atestación.** Documento firmado y determinista que certifica que un módulo, para un destino, superó la verificación, y enumera en qué confía.

**Base de std.** Interfaz del sistema sobre la que se apoya std en hosted: las llamadas al sistema o la biblioteca del sistema.

**Característica experimental.** Característica que solo se usa activada por una directiva explícita, no puede publicarse en el registro y no forma parte de la conformidad.

**Característica obsoleta.** Característica que conserva su significado pero produce un aviso y se retirará en una versión mayor.

**Certificado.** Prueba del solucionador que un comprobador revisa paso a paso.

**Clase de archivo.** Ejecutable, de demostración o de pruebas; cada una llega a una parte distinta del módulo.

**Clase de producto.** Tipo de producto que puede declararse conforme, con los requisitos que debe cumplir: módulo, frontend, verificador, herramienta de mutación, formateador, backend, especificación de destino, cadena de herramientas, biblioteca estándar, gestor de paquetes o registro.

**Código fantasma.** Código de los archivos de demostración que aporta las demostraciones que el solucionador no encuentra solo; se verifica y se borra.

**Comprobación en ejecución.** VC desconocida que se compila como comprobación con aborto.

**Concurrencia estructurada.** Modelo en el que ninguna tarea sobrevive al ámbito que la creó.

**Declaración de conformidad.** Documento público que afirma que un producto es conforme e indica la versión exacta de la especificación, la clase de producto, los perfiles, las extensiones y las decisiones concretas propias.

**Desclasificación.** Conversión de un dato secreto en uno observable, solo en una justificación; queda en la atestación.

**Diff de significado.** Comparación entre versiones que reporta cambios de efectos, contratos, procedencia, errores, telemetría y confianza, no de texto.

**Directiva.** Anotación dirigida a la cadena de herramientas; una sugerencia puede ignorarse y nunca cambia el significado, y una exigencia se verifica.

**Doble compilación diversa.** Construir la cadena de herramientas por dos caminos independientes y exigir binarios idénticos.

**Edición.** Conjunto de cambios de sintaxis de un lenguaje; no cambia la representación intermedia.

**Efecto.** Interacción de una función con algo fuera de su propio cómputo, declarada en su firma.

**Especificación conceptual.** Documento de la etapa de concepto que define por completo el modelo abstracto y nada de lo concreto.

**Especificación de destino.** Declaración de los intrínsecos, el arranque, el aborto y las capacidades de una plataforma. Parte de la TCB.

**Etapa de concepto.** Primera etapa del ciclo de vida de un sistema (ISO/IEC/IEEE 15288), en la que se establecen el concepto, su viabilidad y su conveniencia.

**Extensión.** Función que un producto añade a lo que exige su clase; no contradice ningún requisito ni cambia el resultado de verificar un módulo conforme.

**Freestanding / hosted.** Perfil sin sistema operativo / sobre un sistema operativo.

**Frontera asíncrona.** Conexión con algo que el programa no controla, mediante operaciones que van y vuelven, con un modelo de fallos declarado.

**Frontera del sistema.** Interfaz que el sistema de un destino promete mantener estable; determina en qué se confía y qué puede aislarse.

**Idempotente.** Operación que, aplicada dos veces con los mismos argumentos, produce el mismo estado y la misma respuesta que una vez; se demuestra.

**Identificador de requisito.** Ancla de la sección más el número de orden de un requisito normativo; lo citan las pruebas y las declaraciones de conformidad.

**Informativo.** Contenido que explica o ilustra y no impone requisitos; lo demás es normativo.

**Intrínseco.** Operación primitiva provista por el destino.

**Inventario de confianza.** Lista, en cada atestación, de todo lo que un módulo o binario confía sin demostrarlo.

**IR de bajo nivel.** Sillar: forma SSA sobre un grafo de control con argumentos de bloque, entre Stela verificada y el código del destino; existe solo en compilación.

**Justificación.** Función cuyo contrato demuestra lo necesario para convertir un valor de una etiqueta de procedencia a otra.

**Lema.** Teorema con su demostración, en un archivo de demostración; su recursión con medida es una inducción.

**Modelo de amenazas.** Enumeración de los atacantes contra los que se defiende la plataforma y de la defensa que detiene a cada uno.

**Modelo de fallos.** Fallos que una frontera asíncrona puede exhibir: pérdida, duplicación, reordenamiento, retraso, caída, escritura parcial y corrupción detectable.

**Motor.** Proveedor de tareas: decide cómo se ejecutan las tareas y cómo esperan.

**Mutante.** Variante de una función con un cambio pequeño; queda eliminado solo con un contraejemplo concreto.

**Par externo.** Componente de cualquier lenguaje al otro lado de una frontera asíncrona; si es un binario de la familia con atestación aceptada, es un par verificado.

**Perfil.** Nivel de un destino: core, freestanding o hosted.

**Perfil de optimización.** Objetivo de la optimización de un binario (ninguno, velocidad o tamaño); no cambia el significado y queda en la atestación.

**Plugin.** Módulo verificado cargado en ejecución dentro de un techo de interfaz, efectos y confianza fijado al compilar.

**Presupuesto del solucionador.** Pasos deterministas que el solucionador dedica a una VC antes de declararla desconocida.

**Procedencia.** Etiqueta de tipo que indica de dónde viene un valor y qué puede hacer.

**Proveedor.** Implementación de un servicio (memoria dinámica, tareas, reloj, telemetría) que elige el paquete raíz de un binario.

**Requisito abierto.** Efecto o capacidad que un módulo usa sin proveer; se satisface al enlazar el binario.

**Selección de versión mínima.** Resolución de dependencias que elige, por paquete y versión mayor, el mayor de los mínimos pedidos.

**TCB.** Base de cómputo confiable: el verificador, el núcleo del backend con su validador de traducción y las especificaciones de destino, más toda pasada sin validación que un binario declare en su inventario.

**Teorema de la plataforma.** Propiedad de Stela, Dintel, Cincel o Plomada que la mecanización debe demostrar; mientras no lo esté, es un supuesto enumerado.

**Testigo de capacidad.** Valor de tamaño cero que demuestra que una extensión del procesador está disponible.

**Tiempo constante.** Propiedad de un código cuya duración, accesos a memoria y saltos no dependen de datos secretos.

**Trait.** Conjunto de funciones con contratos que un tipo puede implementar.

**Validación de traducción.** Comprobación, para cada compilación, de que la salida de una pasada preserva el significado de su entrada; la hace Plomada y saca la pasada de la TCB.

**Variante por destino.** Archivo de un módulo que se compila solo para los destinos que cumplen su condición.

**VC.** Condición de verificación: fórmula cuya validez implica que el código cumple una propiedad.

---

← [Fundamentos de diseño](34-fundamentos.md) · [Índice](README.md)
