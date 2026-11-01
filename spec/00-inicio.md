---
title: "Visión general"
order: 0
---
*Fase 0 · Etapa de concepto*

# Dubito

Dubito, ergo compilo.

Dubito es un proyecto de lenguajes de programación verificados: una plataforma de compilación compartida y seis lenguajes que la usan, en la que todo programa se entrega junto con la evidencia de lo que afirma. Ningún módulo se compila hasta que sus efectos, sus contratos y el origen de sus datos están demostrados o comprobados.

La plataforma está formada por una representación intermedia (Stela), un verificador (Dintel), una herramienta de mutación (Speculum), un formateador (Estuco), un backend con su optimizador y su validador de traducción (Cincel, Pulido y Plomada), las especificaciones de destino (Rumbo), una biblioteca estándar (Chinampa) y la cadena de herramientas (dubito). Sobre ella hay una [familia de seis lenguajes](01-familia.md) del mismo rango, cada uno con un paradigma distinto y las mismas garantías.

## <a id="inicio-estado"></a>Estado de este documento *(Informativa)*

| Campo             | Valor                                                                                                                                                                                                                  |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Versión           | 1.0.0-alpha.1                                                                                                                                                                                                                  |
| Estado            | Alpha · especificación conceptual (fase 0)                                                                                                                                                                                        |
| Fecha             | 2026-11-01                                                                                                                                                                                                             |
| Editor            | Ing. Xhunik Nikol Miguel Mutzutz                                                                                                                                                                                       |
| Derechos de autor | © 2026 el editor y los colaboradores de Dubito                                                                                                                                                                         |
| Licencia          | CC BY-SA 4.0 ([Licencias](30-proyecto.md#pro-licencias))                                                                                                                                                               |
| Versión normativa | Español                                                                                                                                                                                                                |
| Comentarios       | Propuestas públicas según el [proceso de gobierno](30-proyecto.md#pro-gobierno)                                                                                                                                        |
| Versionado        | Semantic Versioning 2.0.0, con prelanzamientos alpha, beta y rc hasta la 1.0.0 ([Versiones de la especificación](30-proyecto.md#pro-compat-especificacion)). En alpha cualquier requisito puede cambiar; desde la 1.0.0, solo una versión mayor puede invalidar una declaración de conformidad. |

## <a id="inicio-fase"></a>Fase del proyecto *(Informativa)*

Dubito está en su **fase 0, la etapa de concepto** (*concept stage* en el ciclo de vida de ISO/IEC/IEEE 15288). No existe ninguna implementación.

Este documento es la **especificación conceptual**: define por completo el modelo abstracto (la filosofía, las garantías, la semántica y las reglas que toda implementación debe cumplir) y no inventa nada concreto. Donde la industria ya tiene un estándar, se adopta por referencia. Lo concreto que no está estandarizado (la sintaxis de los lenguajes, los formatos propios, las herramientas y sus comandos, las extensiones de archivo, los códigos de diagnóstico y los valores numéricos) se decidirá en las etapas siguientes, siempre dentro de lo que aquí se fija; cada punto está registrado en el [anexo A](33-anexo-a.md).

Donde ya existe un estándar de la industria, se adopta: la especificación lo cita en [Estándares adoptados](32-estandares.md) y nunca redefine algo estandarizado.

## <a id="inicio-convenciones"></a>Convenciones

Las palabras clave de BCP 14 se escriben en español con esta correspondencia:

| Palabra clave             | Equivale a (BCP 14)   |
|---------------------------|-----------------------|
| **DEBE**, **DEBEN**       | MUST, REQUIRED, SHALL |
| **NO DEBE**, **NO DEBEN** | MUST NOT, SHALL NOT   |
| **PUEDE**, **PUEDEN**     | MAY, OPTIONAL         |

- Las palabras clave tienen ese sentido solo cuando aparecen en mayúsculas, como dispone RFC 8174; en minúsculas tienen su sentido ordinario.
- La especificación no usa los niveles SHOULD ni RECOMMENDED: cada requisito es una obligación o un permiso, sin término medio.
- **Normativo e informativo.** Todo el contenido es normativo salvo la introducción de cada página (el texto entre su título y su primera sección, incluida la línea de rol), el anexo B, las secciones marcadas *(Informativa)*, las figuras y sus leyendas, y los ejemplos. Una introducción resume requisitos que están en las secciones de su página o en otras, y nunca añade uno. En las secciones normativas, los enunciados en indicativo (por ejemplo, «el verificador rechaza el módulo») también son requisitos; las palabras clave marcan las obligaciones y los permisos explícitos.
- **Identificadores de requisitos.** Cada requisito de una sección normativa lleva un identificador formado por el ancla de su sección y su número de orden (por ejemplo, `nuc-tipos-3`), según ISO/IEC/IEEE 29148:2018. Las pruebas y las declaraciones de conformidad citan esos identificadores. Mientras la versión sea un prelanzamiento `alpha` pueden cambiar ([Versiones de la especificación](30-proyecto.md#pro-compat-especificacion)); desde el primer prelanzamiento `beta`, un identificador nunca se reutiliza y un requisito retirado conserva el suyo, marcado como retirado.
- **Referencias.** Cuando el texto cita un estándar sin indicar su edición, rige la edición indicada en [Estándares adoptados](32-estandares.md).
- **Idioma.** La versión normativa es la española ([Idiomas](30-proyecto.md#pro-idiomas)).
- **Conformidad.** Qué productos pueden declararse conformes y cómo se declara está en [Conformidad](31-conformidad.md).

## <a id="inicio-principios"></a>Principios de diseño *(Informativa)*

1.  **Un programa es un argumento.** Firmas, efectos, contratos y etiquetas de procedencia son premisas que el compilador verifica, no anotaciones opcionales.
2.  **Optimizado para revisar, no para escribir.** El código se asume generado en gran parte por herramientas automáticas y revisado por personas. Los cambios se presentan como un diff de significado.
3.  **Toda especificación debe ser falsable.** Un contrato que no distingue la implementación de sus mutaciones se rechaza.
4.  **Confianza mínima y a la vista.** Solo el verificador, el núcleo del backend con su validador de traducción, la especificación de cada destino y la base de la mecanización forman la base de cómputo confiable (TCB), más las pasadas sin validación que un binario declare ([Capas de confianza](26-confianza.md#conf-capas)); todo lo demás se verifica. Lo que un programa confía de su sistema o de código externo es lo mínimo que su destino permite, y queda enumerado.
5.  **Lenguajes del mismo rango.** Ningún lenguaje es el principal. Cada paradigma vive en su propio lenguaje y todos se combinan a través de la plataforma.

## <a id="inicio-invariantes"></a>Invariantes normativas

Toda implementación conforme ([Conformidad](31-conformidad.md)) DEBE cumplir estas reglas. Ninguna característica de un lenguaje, de una biblioteca ni de una herramienta puede contradecirlas.

| Regla   | Enunciado                                                                                                                                                                                                                                                                                                                                                                                                       |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **R1**  | Ninguna garantía depende del entorno de ejecución. Efectos, contratos, ownership y procedencia se verifican en compilación.                                                                                                                                                                                                                                                                                     |
| **R2**  | La plataforma no exige entorno de ejecución: no hay recolector de basura, máquina virtual ni intérprete, y la compilación es anticipada a código nativo. Un lenguaje cuyo modelo necesita soporte en ejecución lo trae como biblioteca verificada.                                                                                                                                                              |
| **R3**  | La representación intermedia existe solo en compilación. Todos los lenguajes de la familia son frontends del mismo rango sobre ella.                                                                                                                                                                                                                                                                            |
| **R4**  | Las bibliotecas añaden capacidades, nunca garantías. Lo que el sistema de verificación necesita expresar pertenece al núcleo.                                                                                                                                                                                                                                                                                   |
| **R5**  | Toda postcondición de código ejecutable DEBE eliminar al menos un mutante. Los lemas son teoremas y quedan fuera de esta regla.                                                                                                                                                                                                                                                                                 |
| **R6**  | Nada implícito en la representación intermedia: no tiene flujo de control, asignaciones de memoria ni conversiones ocultas. Lo que un lenguaje abstrae (despacho virtual, manejadores de efectos, macros) queda explícito en ella y visible en el diff de significado.                                                                                                                                          |
| **R7**  | Cada programa tiene una única forma canónica, de la que se deriva su identidad.                                                                                                                                                                                                                                                                                                                                 |
| **R8**  | Ningún programa puede suspender sus garantías: ningún lenguaje de la familia tiene una construcción insegura ni equivalente.                                                                                                                                                                                                                                                                                    |
| **R9**  | La confianza es mínima, declarada y enumerada. Lo no demostrado solo proviene del destino (su especificación, su sistema y su hardware) o de una frontera declarada en el código; cada atestación enumera exactamente en qué confía, y todo aumento aparece en el diff de significado.                                                                                                                          |
| **R10** | Todo es de tipado estático y explícito: cada valor tiene un tipo conocido en compilación. No existe tipado dinámico ni comprobaciones de tipo implícitas en ejecución, ni inferencia: todo nombre que se introduce declara su tipo y toda instanciación genérica se escribe. Los datos cuya forma solo se conoce al leerlos usan un tipo suma de datos genéricos y se examinan o convierten de forma explícita. |
| **R11** | Todo lenguaje de la familia está disponible en los tres perfiles: core, freestanding (kernels y firmware) y hosted (espacio de usuario). Lo que cambia entre perfiles son sus capacidades, que se adecuan a lo que el destino provee; ningún lenguaje exige un perfil para existir.                                                                                                                             |

## <a id="inicio-pipeline"></a>De la fuente al binario *(Informativa)*

*Figura: diagrama de la cadena de compilación.* Solo lo que está dentro del recuadro punteado necesita confianza durante la compilación: Dintel, el núcleo de Cincel con Plomada y la especificación del destino (Rumbo). La base de la mecanización también pertenece a la TCB, aunque no se ejecuta al compilar ([Capas de confianza](26-confianza.md#conf-capas)). Las pasadas de Pulido sin validación, si se usan, se suman al inventario de confianza. Si un frontend o el código generado contienen errores, Dintel rechaza el módulo antes de que llegue a Cincel.

## <a id="inicio-familia"></a>Lenguajes *(Informativa)*

Seis lenguajes independientes y del mismo rango emiten la misma representación intermedia. Cada uno tiene su paradigma; todos comparten tipos, efectos, contratos y procedencia, así que un mismo proyecto puede combinarlos.

- [**Zea**](03-zea.md): Sistemas: imperativo y funcional, con ownership.
- [**Talud**](04-talud.md): Orientado a objetos con herencia y diseño por contrato.
- [**Solsticio**](05-solsticio.md): Funcional puro: expresiones, recursión, efectos algebraicos.
- [**Voluta**](06-voluta.md): Simbólico: código como dato, macros en compilación, tipos explícitos.
- [**Amate**](07-amate.md): Lógico: hechos y reglas, con explicación de cada conclusión.
- [**Relevo**](08-relevo.md): Actores aislados que se comunican por mensajes, con supervisión.

## <a id="inicio-componentes"></a>Componentes de la plataforma *(Informativa)*

- [**dubito**](09-compilador.md): Cadena de herramientas: frontends, generación de VC y coordinación.
- [**Stela**](10-stela.md): Representación intermedia que lleva su propia evidencia.
- [**Dintel**](12-dintel.md): Verificador de la IR y emisor de atestaciones.
- [**Speculum**](14-speculum.md): Pruebas de mutación de contratos.
- [**Estuco**](17-estuco.md): Formateador de forma canónica.
- [**Ceiba**](28-ceiba.md): Gestor de paquetes con dependencias por hash.
- [**Pochteca**](29-pochteca.md): Registro público de paquetes y atestaciones.
- [**Destinos y perfiles**](20-destinos.md): Perfiles, disponibilidad y concurrencia en cada destino.
- [**Modelo de confianza**](26-confianza.md): Qué se confía en cada destino, cómo se reduce y cómo queda enumerado.
- [**Chinampa**](21-chinampa.md): Biblioteca estándar en tres capas.
- [**Sillar**](11-sillar.md): IR de bajo nivel en forma SSA, entre Stela y el código del destino.
- [**Pulido**](15-pulido.md): Optimizador que no cambia el significado.
- [**Plomada**](13-plomada.md): Validador de traducción de cada pasada.
- [**Cincel**](16-cincel.md): Backend: de la IR verificada al código del destino.
- [**Glosa**](18-glosa.md): Diff de significado para la revisión.
- [**Rumbo**](19-rumbo.md): Especificaciones de destino.
- [**Modelo de amenazas**](27-amenazas.md): Contra quién se defiende la plataforma.

## <a id="inicio-aportes"></a>Aportes *(Informativa)*

Cuatro elementos son la contribución específica del proyecto; el resto de las decisiones adopta soluciones ya probadas:

1.  La adecuación por mutación como regla de compilación (R5).
2.  La procedencia unificada de datos, con datos secretos de tiempo constante y protecciones de especulación dirigidas.
3.  El diff de significado de efectos, contratos, procedencia y telemetría como forma principal de revisión.
4.  Una familia de lenguajes de paradigmas distintos, sin ninguna construcción que suspenda garantías, sobre una sola representación intermedia que lleva su evidencia.

---

[Índice](README.md) · [Familia de lenguajes](01-familia.md) →
