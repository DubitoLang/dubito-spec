<!--
SPDX-FileCopyrightText: 2026 Xhunik Nikol Miguel Mutzutz y colaboradores de Dubito
SPDX-License-Identifier: CC-BY-SA-4.0
-->

# Registro de cambios

Todos los cambios notables de la especificación se registran aquí. El formato sigue [Keep a Changelog 1.1.0](https://keepachangelog.com/es-ES/1.1.0/) y las versiones siguen [Semantic Versioning 2.0.0](https://semver.org/lang/es/).

## [Sin publicar]

Correcciones de la revisión independiente de cierre de la fase 0.

### Cambiado

### Corregido

- Enlaces de comparación al final de este registro y etiqueta `v1.0.0-alpha.1` sobre el commit de la versión publicada.

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
