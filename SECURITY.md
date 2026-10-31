<!--
SPDX-FileCopyrightText: 2026 Xhunik Nikol Miguel Mutzutz y colaboradores de Dubito
SPDX-License-Identifier: CC-BY-SA-4.0
-->

# Seguridad

La gestión de vulnerabilidades sigue ISO/IEC 29147:2018 (divulgación) e ISO/IEC 30111:2019 (tratamiento). El texto normativo está en [Seguridad y vulnerabilidades](spec/30-proyecto.md#pro-seguridad).

## Cómo reportar

Reporta las vulnerabilidades **en privado** con el reporte privado de vulnerabilidades de GitHub (pestaña *Security* → *Report a vulnerability*). No abras un issue público mientras no haya corrección.

## Qué es una vulnerabilidad

En la fase 0 no hay código: una vulnerabilidad es un error del texto que permite que una implementación conforme sea insegura. En particular, es de máxima gravedad cualquier error que permita aceptar un programa que no cumple su atestación (en la especificación de Dintel, Cincel, Plomada, Rumbo o la mecanización), aunque no se conozca un ataque.

## Proceso

- La gravedad se puntúa con CVSS 4.0.
- El plazo de divulgación se acuerda con quien reporta, y se le reconoce si lo desea.
- Cada vulnerabilidad recibe un identificador CVE y se publica como aviso en OSV y en CSAF 2.0.
