<!--
SPDX-FileCopyrightText: 2026 Xhunik Nikol Miguel Mutzutz y colaboradores de Dubito
SPDX-License-Identifier: CC-BY-SA-4.0
-->

# Dubito

*Dubito, ergo compilo.*

Dubito es un proyecto de lenguajes de programación verificados: una plataforma de compilación compartida y seis lenguajes del mismo rango (Zea, Talud, Solsticio, Voluta, Amate y Relevo) en la que todo programa se entrega junto con la evidencia de lo que afirma.

> **Estado: fase 0, etapa de concepto.** Este repositorio contiene la especificación conceptual 1.0.0-alpha.1. **No existe ninguna implementación.** La especificación define por completo el modelo abstracto y deja sin definir todo lo concreto (sintaxis, formatos y herramientas), que se decidirá en las etapas siguientes.

## Contenido

| Ruta | Qué es |
|---|---|
| [`spec/`](spec/README.md) | La especificación, una página por archivo. Es la fuente normativa. |
| [Sitio](https://dubitolang.github.io/dubito-spec/) | GitHub Pages lo genera automáticamente desde `spec/` con Jekyll en cada cambio de `main`. |
| [`CHANGELOG.md`](CHANGELOG.md) | Registro de cambios por versión. |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Cómo proponer cambios y el Developer Certificate of Origin. |
| [`GOVERNANCE.md`](GOVERNANCE.md) | Quién decide y cómo se aprueban los cambios. |
| [`SECURITY.md`](SECURITY.md) | Cómo reportar una vulnerabilidad. |
| [`TRADEMARKS.md`](TRADEMARKS.md) | Uso de los nombres y logos del proyecto. |
| [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md) | Código de conducta. |

## Por dónde empezar

1. [Visión general](spec/00-inicio.md): fase, principios e invariantes R1–R11.
2. [Familia de lenguajes](spec/01-familia.md) y [Núcleo común](spec/02-nucleo.md).
3. [Conformidad](spec/31-conformidad.md): qué significa implementar esta especificación.

## Editar y construir el sitio

El texto vive solo en `spec/`, en Markdown. Cada archivo empieza con un bloque de metadatos (título y marca de componente) que no se edita a mano. Al integrar un cambio en `main`, GitHub Pages construye el sitio con Jekyll y lo publica.

Para verlo en local: `bundle install` y luego `bundle exec jekyll serve`.

## Idioma

La especificación se publica en español, que es su versión normativa. Las palabras de los lenguajes (palabras reservadas, nombres de la biblioteca y valores predefinidos) están siempre en inglés.

## Licencia

El texto de la especificación se publica bajo [CC BY-SA 4.0](LICENSES/CC-BY-SA-4.0.txt). Implementar la especificación no es una obra derivada del texto. Las licencias de las futuras herramientas y bibliotecas están en [Licencias](spec/30-proyecto.md#pro-licencias). El repositorio sigue la especificación [REUSE](https://reuse.software).

Los nombres y logos del proyecto no están cubiertos por la licencia: ver [TRADEMARKS.md](TRADEMARKS.md).
