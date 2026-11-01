<!--
SPDX-FileCopyrightText: 2026 Xhunik Nikol Miguel Mutzutz y colaboradores de Dubito
SPDX-License-Identifier: CC-BY-SA-4.0
-->

# Registro de cambios

Todos los cambios notables de la especificación se registran aquí. El formato sigue [Keep a Changelog 1.1.0](https://keepachangelog.com/es-ES/1.1.0/) y las versiones siguen [Semantic Versioning 2.0.0](https://semver.org/lang/es/).

## [1.0.0-alpha.1] - 2026-11-01

Primera versión publicada: la especificación conceptual completa, con la que se cierra la fase 0. La numeración 0.1.0 que se usó internamente antes de publicar se descarta; la política de versiones está en [Compatibilidad](spec/30-proyecto.md#pro-compatibilidad).

### Añadido

- Especificación conceptual de la fase 0 en 36 páginas y siete grupos: invariantes R1–R11, núcleo común, los seis lenguajes (Zea, Talud, Solsticio, Voluta, Amate y Relevo), la plataforma (Stela, Sillar, Dintel, Plomada, Speculum, Estuco, Pulido, Cincel, Glosa, Rumbo y Chinampa) y el ecosistema (Ceiba y Pochteca).
- Convenciones: palabras clave de BCP 14 en español, contenido normativo e informativo (las introducciones de página y las líneas de rol son informativas) e identificadores de requisito según ISO/IEC/IEEE 29148, con ancla enlazable para cada requisito, invariante y teorema.
- Una sola definición de la TCB en [Capas de confianza](spec/26-confianza.md#conf-capas): Dintel, el núcleo de Cincel con Plomada, las especificaciones de destino, la base de la mecanización y las pasadas sin validación que un binario declare.
- Nueve teoremas obligatorios de la plataforma, mecanizados sobre las semánticas de Stela, de Sillar y de la arquitectura de cada destino, con su modelo de fugas.
- Dintel como verificador que solo comprueba evidencia, incluida la evidencia de mutación; atestaciones de módulo, de enlace y de binario.
- Plomada como validador de las pasadas de optimización sobre Sillar; el núcleo de Cincel queda cubierto por T7.
- Construcción de la propia cadena: compilación reproducible y doble compilación diversa según Wheeler.
- Perfiles core, freestanding y hosted, con la definición de lo que significa que un lenguaje esté disponible en los tres (R11).
- Cláusula de conformidad con catorce clases de producto, declaración de conformidad, métodos de verificación de ISO/IEC/IEEE 29148 y plan del conjunto de pruebas.
- Modelo de amenazas, anexo A (definido por el destino, definido por la implementación y pendiente de definir por la especificación), anexo B (fundamentos de diseño) y glosario.
- Estándares adoptados con sus ediciones normativas.
- Criterios de salida de la fase 0 en [Fases](spec/30-proyecto.md#pro-fase).
- Gobierno, contribuciones, política de vulnerabilidades, ciclo de vida de las características, política de marca, licencias (incluidas las de la mecanización y las especificaciones de destino) y política de versiones de la especificación, con los eventos que abren `beta` y `rc`.
- Archivos del repositorio: `LICENSE` (CC BY-SA 4.0), `CONTRIBUTING.md`, `GOVERNANCE.md`, `SECURITY.md`, `TRADEMARKS.md`, `CODE_OF_CONDUCT.md`, `CITATION.cff` y metadatos REUSE.
- [Roadmap](ROADMAP.md) informativo, fuera de `spec/`, con las fases de la especificación conceptual a la 1.0.0.
- Sitio generado con Jekyll a partir del Markdown de `spec/`, que es la única fuente.

[1.0.0-alpha.1]: https://github.com/DubitoLang/dubito-spec/releases/tag/v1.0.0-alpha.1
