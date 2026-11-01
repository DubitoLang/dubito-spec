<!--
SPDX-FileCopyrightText: 2026 Xhunik Nikol Miguel Mutzutz y colaboradores de Dubito
SPDX-License-Identifier: CC-BY-SA-4.0
-->

# Registro de cambios

Todos los cambios notables de la especificación se registran aquí. El formato sigue [Keep a Changelog 1.1.0](https://keepachangelog.com/es-ES/1.1.0/) y las versiones siguen [Semantic Versioning 2.0.0](https://semver.org/lang/es/).

## [Sin publicar]

Correcciones de la revisión independiente de cierre de la fase 0.

### Cambiado
- Anexo A: ahora distingue tres categorías (definido por el destino, por la implementación y pendiente de definir por la especificación) y registra todo lo concreto que faltaba: orden de bytes, punto flotante, aborto, formato ejecutable, protecciones de especulación, ventana especulativa, fronteras asíncronas y reducción de privilegios (destino); presupuesto de la evaluación en compilación (implementación); y dieciséis puntos pendientes, entre ellos la sintaxis, las codificaciones, los formatos de atestación, testigo, evidencia de mutación, especificación de destino, inventario, manifiestos y protocolo del registro, el contenido de Chinampa y el asistente de pruebas. Nuevos requisitos `anx-reglas-5` y `anx-reglas-6`.
- TCB: se define en un solo lugar, [Capas de confianza](spec/26-confianza.md#conf-capas), y ahora incluye la base de la mecanización (núcleo del asistente de pruebas y definiciones mecanizadas), nueva capa `conf-capas-6`. La visión general, Dintel (`dintel-tcb-2`, nuevo `dintel-tcb-5`), los niveles de representación y el glosario remiten a esa definición y hablan del núcleo de Cincel, no del backend entero. Nuevo requisito `conf-capas-7`.
- Teoremas T6 y T7: se demuestran para cada destino sobre la semántica mecanizada de su arquitectura y su modelo de fugas. Toda especificación de destino de referencia o revisada incluye esa semántica, adoptada por referencia si existe una oficial (nuevo `dst-spec-14`); `stx-teoremas-1` y `anx-destino-7` lo recogen.
- Perfiles: una especificación de destino declara freestanding o hosted; core es el perfil de los módulos que no invocan intrínsecos y se compilan para cualquier destino (nuevo `dst-perfiles-7`). Ese requisito define qué significa estar disponible en los tres perfiles (R11), y lo usan `dst-spec-2`, `pro-compatibilidad-10` y `cnf-requisitos-2`, que ahora exige a frontends y verificadores admitir los tres perfiles. Nueva entrada «Core» en el glosario.
- Clases de conformidad: el Verificador incluye el Núcleo común, la disponibilidad por destino y la interoperabilidad; el Frontend, la interoperabilidad entre lenguajes; el Backend, la especificación de destino, las obligaciones de tiempo constante y especulación y la depuración. Nuevas clases Optimizador de Stela (`cnf-clases-14`) y Mecanización (`cnf-clases-15`).

### Corregido
- Enlaces de comparación al final de este registro y etiqueta `v1.0.0-alpha.1` sobre el commit de la versión publicada.
- `bootstrap-4` describía la doble compilación diversa como si dos cadenas independientes debieran producir los mismos bytes, lo que no puede cumplirse. Ahora sigue el método de Wheeler: lo que coincide bit a bit es la recompilación hecha por el compilador intermedio con el binario oficial. El glosario se corrige igual.
- Dintel ya no busca: `dintel-pasos-8` comprueba la evidencia de mutación en lugar de repetir la mutación, `dintel-pasos-7` exige que toda suposición provenga de la especificación del destino, y `dintel-tcb-4` precisa que comprobar evidencia incluye evaluar contraejemplos pero nunca buscar. El contraejemplo de un mutante es una entrada que se comprueba evaluando con la semántica de Stela, sin generar código (`elk-criterio-1`), lo que elimina la dependencia circular con el backend. La comprobación de vacuidad pasa a la cadena de herramientas como diagnóstico (`nuc-limites-24`), y la consistencia de una especificación de destino se comprueba al admitirla (`dst-gobierno-6`).
- Las convenciones seguían diciendo que los identificadores pueden cambiar «mientras la versión sea 0.y.z»; ahora siguen la política de prelanzamientos: pueden cambiar en `alpha` y son estables desde `beta`.
- `cnf-declaracion-9` decía que una declaración de conformidad vale solo para su versión exacta, contra `pro-compatibilidad-12` y la ficha. Ahora vale solo para su versión mientras sea un prelanzamiento, y desde la 1.0.0 para toda la misma versión mayor.
- `pro-compatibilidad-7` definía el parche como ningún cambio en la interfaz pública, aunque la documentación forma parte de ella y cambiarla es un parche (`nuc-documentacion-2`). Ahora exceptúa la documentación.
- Alcance de Plomada: valida las pasadas de optimización sobre Sillar; la bajada y el resto del núcleo de Cincel pertenecen a la TCB y los cubre T7. Se alinean la introducción de Plomada, `sillar-semantica-2`, `plomada-proceso-3`, `niveles-4`, T7 y T8 (los puntos de telemetría pasan a figurar en T7, y los efectos y su orden en T8).
- `optimizacion-3` decía que toda pasada DEBE tener validación y en la misma celda admitía pasadas sin ella; ahora una pasada PUEDE no tener validación si figura en el inventario de confianza.
- `cnf-pruebas-2` exigía una prueba por cada identificador, imposible para los requisitos de proceso, de mecanización o descriptivos. Ahora cada requisito tiene un método de verificación de ISO/IEC/IEEE 29148 (inspección, análisis, demostración o prueba). Se precisan requisitos que no podían verificarse: `fam-sintaxis-3`, `fam-sintaxis-4`, `fam-objetivos-11`, `dintel-tcb-4`, `obs-senales-2` y `conf-principios-2`.









## [1.0.0-alpha.1] - 2026-11-01

Primera versión de la línea oficial. La numeración 0.1.0 que se usó internamente antes de publicar se descarta; la política de versiones está en [Compatibilidad](spec/30-proyecto.md#pro-compatibilidad).

### Añadido

- Especificación conceptual completa de la fase 0: invariantes R1–R11, núcleo común, los seis lenguajes, la plataforma (Stela, Sillar, Dintel, Plomada, Speculum, Estuco, Pulido, Cincel, Glosa, Rumbo y Chinampa) y el ecosistema (Ceiba y Pochteca).
- Una página por componente, en 36 páginas y siete grupos, con identificadores de requisito estables.
- Sitio generado con Jekyll a partir del Markdown de `spec/`, que es la única fuente.
- Convenciones: palabras clave de BCP 14 en español, contenido normativo e informativo e identificadores de requisitos según ISO/IEC/IEEE 29148.
- Cláusula de conformidad, con clases de producto, declaración de conformidad y plan del conjunto de pruebas.
- Modelo de amenazas, nueve teoremas obligatorios de la plataforma, anexo A (definido por el destino o la implementación) y anexo B (fundamentos de diseño).
- Sillar: SSA sobre un grafo de control con argumentos de bloque (sin nodos phi), instrucciones de resultado único y exactamente un terminador por bloque; semántica operacional mecanizada que Plomada compara con la de Stela; y técnicas internas de las pasadas, que pueden usar otra representación siempre que entreguen Sillar y pasen por Plomada o se declaren en el inventario de confianza.
- Anexo A: la codificación de Stela y de Sillar puede ser textual o binaria; la de Sillar DEBE ser determinista para que la construcción sea reproducible.
- Estándares adoptados con sus ediciones normativas.
- Criterios de salida de la fase 0 en [Fases](spec/30-proyecto.md#pro-fase).
- Archivo `LICENSE` en la raíz del repositorio con la licencia del texto (CC BY-SA 4.0), y pie del sitio con el aviso de derechos y la licencia.
- Gobierno, contribuciones, política de vulnerabilidades, ciclo de vida de las características, política de marca, licencias y política de versiones de la especificación.

### Cambiado

- Los nombres de los trece componentes (Solsticio, Amate, Dintel, Estuco, Pochteca, Quelonio, Sillar, Plomada, Pulido, Cincel, Glosa, Rumbo y Chinampa) quedan confirmados por el editor. No se hizo una búsqueda formal de marcas; si más adelante aparece un conflicto, se cambia el nombre en una versión posterior.
- Conformidad: la clase Backend incluye ahora Sillar y Plomada entre sus requisitos, y existe la clase Herramienta de revisión (Glosa, R6).
- Teoremas de la plataforma: la mecanización cubre las semánticas de Stela y de Sillar, porque T7 y T8 se apoyan en ambas.
- Glosario: 21 entradas nuevas con los nombres de los seis lenguajes y de los componentes, la mascota y el nombre del proyecto.

### Corregido

- La ficha de la especificación y el requisito `cnf-requisitos-5` seguían refiriéndose a versiones 0.y.z; ahora citan los prelanzamientos y la política de versiones.
- Se revisó la edición de in-toto citada en los estándares adoptados: la 1.2.0 es la versión vigente, sin cambios.

### Revisión de cierre de la fase 0

Comprobaciones hechas sobre las 36 páginas: ningún identificador duplicado ni con huecos, ningún enlace ni ancla rotos, cadena de anterior y siguiente íntegra, índice completo, ninguna referencia a nombres anteriores, a palabras SHOULD o a lenguajes y destinos concretos, y coherencia entre la TCB, los teoremas T1–T9, las invariantes R1–R11, el Anexo A y las clases de conformidad. Los hallazgos están resueltos en las entradas anteriores.

[Sin publicar]: https://github.com/DubitoLang/dubito-spec/compare/v1.0.0-alpha.1...HEAD
[1.0.0-alpha.1]: https://github.com/DubitoLang/dubito-spec/releases/tag/v1.0.0-alpha.1
