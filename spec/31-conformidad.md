---
title: "Conformidad"
order: 31
---
*Referencia*

# Conformidad

Qué productos pueden declararse conformes con esta especificación, qué requisitos se aplican a cada uno y cómo se declara. Sigue el marco de calidad del W3C para especificaciones.

## <a id="cnf-clases"></a>Clases de producto

<a id="cnf-clases-1"></a>Cada clase reúne los requisitos normativos que le aplican. Un mismo producto puede pertenecer a varias clases y DEBE cumplir los requisitos de cada una. Los nombres de los componentes designan las piezas del proyecto; una implementación independiente puede ocupar la misma clase con otro nombre ([Política de marca](30-proyecto.md#pro-marca)). `cnf-clases-1`

| Clase                                    | Qué es                                                      | Requisitos                                                                                                                                                                                                                                     |
|------------------------------------------|-------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Módulo `cnf-clases-2`                    | Unidad compilada de cualquier lenguaje de la familia.       | Es conforme si un verificador conforme lo acepta para un destino conforme.                                                                                                                                                                     |
| Frontend `cnf-clases-3`                  | Traductor de un lenguaje de la familia a Stela.             | [Núcleo común](02-nucleo.md); la página de su lenguaje; [principios de sintaxis](01-familia.md#fam-sintaxis) y [criterio de admisión](01-familia.md#fam-admision); [criterios de sintaxis](01-familia.md#fam-criterios); [Stela](10-stela.md); [Interoperabilidad entre lenguajes de la familia](25-interop.md#int-familia). |
| Verificador `cnf-clases-4`               | Decide si un módulo se acepta y emite su atestación.        | [Núcleo común](02-nucleo.md); [Stela](10-stela.md); [Dintel](12-dintel.md); [Disponibilidad](20-destinos.md#dst-disp); [Interoperabilidad](25-interop.md); [Modelo de confianza](26-confianza.md). |
| Herramienta de mutación `cnf-clases-5`   | Genera mutantes y comprueba la adecuación de los contratos. | [Speculum](14-speculum.md); R5.                                                                                                                                                                                                                |
| Formateador `cnf-clases-6`               | Da su forma canónica al código fuente.                      | [Estuco](17-estuco.md); R7.                                                                                                                                                                                                                    |
| Backend `cnf-clases-7`                   | Baja Stela verificada, la optimiza y genera código nativo.  | [Cincel](16-cincel.md#dst-backend); [Niveles de representación](09-compilador.md#niveles); [Sillar](11-sillar.md); [Plomada](13-plomada.md); [Optimización](15-pulido.md#optimizacion); [Contenido de una especificación de destino](19-rumbo.md#dst-spec); [Datos secretos y tiempo constante](02-nucleo.md#nuc-secretos) y [Ejecución especulativa](02-nucleo.md#nuc-secretos-especulacion) en lo que obligan al backend; [Depuración](09-compilador.md#depuracion); R2.                                                                                                      |
| Especificación de destino `cnf-clases-8` | Declaración de una plataforma y sus perfiles.               | [Rumbo](19-rumbo.md#dst-spec); [Destinos](20-destinos.md); [Adaptar un destino](26-confianza.md#conf-destinos).                                                                                                                                |
| Cadena de herramientas `cnf-clases-9`    | Conjunto que coordina frontends, verificación y backend.    | [dubito](09-compilador.md), incluidas las [directivas](09-compilador.md#directivas); cada componente que distribuye DEBE ser conforme en su clase.                                                                                             |
| Biblioteca estándar `cnf-clases-10`      | Capas que un perfil ofrece a los programas.                 | [Chinampa](21-chinampa.md); [Errores y aborto](22-errores.md); [Entrada y salida](23-es.md); [Observabilidad](24-observabilidad.md); para el perfil que declara.                                                                               |
| Gestor de paquetes `cnf-clases-11`       | Resuelve dependencias y regenera módulos.                   | [Ceiba](28-ceiba.md); [Versiones de un paquete](30-proyecto.md#pro-compat-paquetes).                                                                                                                                                           |
| Registro `cnf-clases-12`                 | Publica y distribuye paquetes.                              | [Pochteca](29-pochteca.md).                                                                                                                                                                                                                    |
| Herramienta de revisión `cnf-clases-13` | Compara dos versiones de un programa por su significado. | [Glosa](18-glosa.md); R6. |
| Optimizador de Stela `cnf-clases-14`     | Transforma Stela en Stela antes del backend.                | [Optimización](15-pulido.md#optimizacion); [Stela](10-stela.md); R6. Su resultado lleva su evidencia y lo verifica un verificador conforme. |
| Mecanización `cnf-clases-15`             | Semánticas formales y teoremas de la plataforma en un asistente de pruebas. | [Stela](10-stela.md); [Semántica de Sillar](11-sillar.md#sillar-semantica); [Teoremas de la plataforma](10-stela.md#stx-teoremas); la semántica de la arquitectura y el modelo de fugas de cada destino ([Contenido de una especificación](19-rumbo.md#dst-spec)). |

## <a id="cnf-requisitos"></a>Requisitos generales

- <a id="cnf-requisitos-1"></a>**Requisitos de la clase.** Un producto conforme DEBE cumplir todos los requisitos normativos de su clase y las invariantes R1–R11 que le aplican. `cnf-requisitos-1`
- <a id="cnf-requisitos-2"></a>**Sin conformidad parcial.** Un producto que incumple un requisito de su clase no es conforme. La única variación admitida es el perfil de destino en las clases Backend, Especificación de destino y Biblioteca estándar, que declaran para qué perfiles son conformes. Un frontend y un verificador DEBEN admitir los tres perfiles (R11, [Perfiles](20-destinos.md#dst-perfiles)). `cnf-requisitos-2`
- <a id="cnf-requisitos-3"></a>**Extensiones.** Un producto PUEDE ofrecer extensiones. Una extensión NO DEBE contradecir ningún requisito, suspender garantías (R8), cambiar el resultado de verificar un módulo conforme ni alterar la identidad de un módulo. Todo lo que una extensión añade a un programa DEBE quedar explícito en la representación intermedia y visible en el diff de significado (R6). `cnf-requisitos-3`
- <a id="cnf-requisitos-4"></a>**Características experimentales.** Un producto conforme puede ofrecerlas solo detrás de su directiva de activación; nada experimental forma parte de su conformidad ([Ciclo de vida](30-proyecto.md#pro-ciclo)). `cnf-requisitos-4`
- <a id="cnf-requisitos-5"></a>**Lo que esta versión no define.** Cuando un producto necesita algo concreto que la especificación todavía no fija (sintaxis, formatos propios, interfaces de herramientas), su elección DEBE documentarse y NO DEBE contradecir ningún requisito. Mientras la versión sea un prelanzamiento alpha, esas elecciones no forman parte de la conformidad. `cnf-requisitos-5`

## <a id="cnf-declaracion"></a>Declaración de conformidad

<a id="cnf-declaracion-1"></a>Quien presenta un producto como conforme DEBE publicar una declaración de conformidad que indique: `cnf-declaracion-1`

- <a id="cnf-declaracion-2"></a>la versión exacta de la especificación (x.y.z, con su prelanzamiento si lo tiene); `cnf-declaracion-2`
- <a id="cnf-declaracion-3"></a>la clase o las clases de producto; `cnf-declaracion-3`
- <a id="cnf-declaracion-4"></a>los perfiles de destino, en las clases que dependen de ellos; `cnf-declaracion-4`
- <a id="cnf-declaracion-5"></a>las extensiones que ofrece; `cnf-declaracion-5`
- <a id="cnf-declaracion-6"></a>la versión del conjunto de pruebas de conformidad que pasa, con sus resultados; `cnf-declaracion-6`
- <a id="cnf-declaracion-7"></a>las decisiones concretas que tomó donde la especificación no las fija; `cnf-declaracion-7`
- <a id="cnf-declaracion-8"></a>la fecha de la declaración. `cnf-declaracion-8`

<a id="cnf-declaracion-9"></a>Una declaración se hace sobre la versión exacta que indica. Mientras esa versión sea un prelanzamiento, vale solo para ella. Desde la 1.0.0, sigue valiendo para las versiones posteriores con la misma versión mayor, que no invalidan las implementaciones conformes ([Versiones de la especificación](30-proyecto.md#pro-compat-especificacion)); una versión mayor nueva exige una declaración nueva. `cnf-declaracion-9`

## <a id="cnf-pruebas"></a>Conjunto de pruebas de conformidad

- <a id="cnf-pruebas-1"></a>El proyecto mantiene un conjunto público de pruebas de conformidad, documentado según ISO/IEC/IEEE 29119-3:2021. `cnf-pruebas-1`
- <a id="cnf-pruebas-2"></a>Cada requisito con identificador tiene asignado uno de los métodos de verificación de ISO/IEC/IEEE 29148: inspección, análisis, demostración o prueba. Los que se verifican por prueba tienen al menos una en el conjunto, y cada prueba cita los identificadores que comprueba; la trazabilidad se publica en los dos sentidos. Los requisitos que obligan al proyecto o a su proceso (versiones, gobierno, admisión de especificaciones de destino), los que se cumplen en la mecanización y las filas descriptivas de las tablas de clasificación se verifican por inspección o por análisis, y la matriz de trazabilidad lo indica. `cnf-pruebas-2`
- <a id="cnf-pruebas-3"></a>Las pruebas negativas, que exigen rechazar un módulo, son tan obligatorias como las positivas: un verificador que acepta lo que DEBE rechazar no es conforme. `cnf-pruebas-3`
- <a id="cnf-pruebas-4"></a>Cada clase de debilidad del [modelo de amenazas](27-amenazas.md#ame-debilidades) tiene pruebas propias. `cnf-pruebas-4`
- <a id="cnf-pruebas-5"></a>Pasar el conjunto es necesario pero no suficiente: la conformidad es con los requisitos, no con las pruebas. `cnf-pruebas-5`
- <a id="cnf-pruebas-6"></a>Cada versión de la especificación indica la versión del conjunto de pruebas que le corresponde. `cnf-pruebas-6`

## <a id="cnf-fase"></a>Conformidad en la fase 0

<a id="cnf-fase-1"></a>En la fase 0 no existe ninguna implementación. La conformidad de las clases que dependen de lo concreto (frontends y formateador, que necesitan una sintaxis) solo podrá comprobarse cuando esa parte se defina. Esta cláusula fija desde ahora qué significará ser conforme, y las etapas siguientes completan los requisitos de cada clase sin cambiar los requisitos generales. `cnf-fase-1`

---

← [Proyecto e identidad](30-proyecto.md) · [Índice](README.md) · [Estándares adoptados](32-estandares.md) →
