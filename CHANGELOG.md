<!--
SPDX-FileCopyrightText: 2026 Xhunik Nikol Miguel Mutzutz y colaboradores de Dubito
SPDX-License-Identifier: CC-BY-SA-4.0
-->

# Registro de cambios

Todos los cambios notables de la especificación se registran aquí. El formato sigue [Keep a Changelog 1.1.0](https://keepachangelog.com/es-ES/1.1.0/) y las versiones siguen [Semantic Versioning 2.0.0](https://semver.org/lang/es/).

## [Sin publicar]

### Añadido

- Sillar: semántica operacional mecanizada (`sillar-semantica`), que Plomada compara con la de Stela; y técnicas internas de las pasadas (`sillar-pulido`): una pasada puede usar otra representación por dentro, pero lo que entrega es Sillar y pasa por Plomada o se declara en el inventario de confianza.
- Sitio de la especificación generado con Jekyll a partir del Markdown de `spec/`, que es la única fuente.

### Cambiado

- Cada componente tiene su página: Sillar, Pulido, Plomada, Cincel, Glosa, Rumbo y Chinampa dejan de ser secciones de otras páginas. Son 36 páginas en siete grupos y se conservan todos los identificadores de requisito.
- Destinos y perfiles conserva solo lo general (perfiles, disponibilidad y concurrencia).
- Sillar: la forma pasa de «código de tres direcciones en SSA» a SSA sobre un grafo de control con argumentos de bloque (sin nodos phi), instrucciones de resultado único y exactamente un terminador por bloque. La tabla de niveles, el glosario y los estándares adoptados se ajustan.
- Anexo A: la codificación de Stela y de Sillar puede ser textual o binaria; la de Sillar DEBE ser determinista para que la construcción sea reproducible.
- El estado del documento deja de ser «borrador»: el texto es la línea oficial de la especificación.

## [0.1.0] - 2026-10-28

### Añadido

- Especificación conceptual completa de la fase 0: invariantes R1–R11, núcleo común, los seis lenguajes, la plataforma (Stela, Sillar, Dintel, Plomada, Speculum, Estuco, Pulido, Cincel, Glosa, Rumbo y Chinampa) y el ecosistema (Ceiba y Pochteca).
- Convenciones: palabras clave de BCP 14 en español, contenido normativo e informativo e identificadores de requisitos según ISO/IEC/IEEE 29148.
- Cláusula de conformidad, con clases de producto, declaración de conformidad y plan del conjunto de pruebas.
- Modelo de amenazas, nueve teoremas obligatorios de la plataforma, anexo A (definido por el destino o la implementación) y anexo B (fundamentos de diseño).
- Estándares adoptados con sus ediciones normativas.
- Gobierno, contribuciones, política de vulnerabilidades, ciclo de vida de las características, política de marca y licencias.
