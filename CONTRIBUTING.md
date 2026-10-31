<!--
SPDX-FileCopyrightText: 2026 Xhunik Nikol Miguel Mutzutz y colaboradores de Dubito
SPDX-License-Identifier: CC-BY-SA-4.0
-->

# Cómo contribuir

Gracias por tu interés en Dubito. El proyecto está en la fase 0: las contribuciones son cambios a la especificación.

## Antes de empezar

- Lee la [Visión general](spec/00-inicio.md) y las [Convenciones](spec/00-inicio.md#inicio-convenciones). Las palabras DEBE, NO DEBE y PUEDE tienen el sentido de BCP 14 solo en mayúsculas.
- Un cambio sustantivo empieza como **propuesta pública** (plantilla «Propuesta»), con un periodo de comentarios, y se aprueba por consenso tácito según [GOVERNANCE.md](GOVERNANCE.md).
- Las correcciones menores (erratas, enlaces, redacción sin cambio de significado) pueden ir directamente en un pull request.
- Cambiar una invariante R1–R11 exige el acuerdo de todos los mantenedores.

## Reglas del texto

- Solo la versión final: la especificación no guarda historial ni alternativas descartadas en el cuerpo normativo; las decisiones y su justificación van en el [anexo B](spec/28-fundamentos.md).
- Donde exista un estándar de la industria, se adopta por referencia y se registra en [Estándares adoptados](spec/26-estandares.md); nunca se redefine.
- Nada concreto sin estándar (sintaxis, formatos propios, herramientas, valores numéricos) se fija en la fase 0.
- La especificación no nombra otros lenguajes de programación ni destinos concretos.
- Cada archivo conserva su cabecera REUSE.

## Developer Certificate of Origin

Cada commit DEBE llevar la firma del [Developer Certificate of Origin 1.1](https://developercertificate.org): al firmar certificas que tienes derecho a aportar ese trabajo con la licencia del proyecto. No se pide cesión de derechos ni acuerdo de contribución.

```
git commit -s
```

añade la línea `Signed-off-by: Nombre <correo>` con el nombre y el correo de tu configuración de git.

Las contribuciones se reciben bajo la misma licencia del archivo al que se aportan (CC BY-SA 4.0 para la especificación).

## Registro de cambios

Todo cambio visible se anota en la sección «Sin publicar» de [CHANGELOG.md](CHANGELOG.md), con el formato de Keep a Changelog.
