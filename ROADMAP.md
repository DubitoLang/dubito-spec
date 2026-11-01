<!--
SPDX-FileCopyrightText: 2026 Xhunik Nikol Miguel Mutzutz y colaboradores de Dubito
SPDX-License-Identifier: CC-BY-SA-4.0
-->

# Roadmap

*(Informativo)* Este documento no forma parte de la especificación y puede cambiar sin una versión nueva de ella. A diferencia de la especificación, nombra destinos concretos.

## Principios

- Cada fase termina con un criterio de salida verificable, y las fases se alinean con los prelanzamientos de la especificación ([Versiones de la especificación](spec/30-proyecto.md#pro-compat-especificacion)): `alpha` cubre las fases 0 a 3, `beta` la fase 4 y `rc` la fase 5.
- Hasta el auto-hospedaje se trabaja con un solo lenguaje, Zea; los otros cinco llegan después, de uno en uno.
- Primero se construye lo que pertenece a la TCB (Dintel, el núcleo de Cincel y Plomada) y después el resto.
- La mecanización avanza en paralelo a las fases; T7, el teorema más costoso, queda para el final. Mientras un teorema no esté mecanizado, figura como supuesto en el inventario de confianza (`stx-teoremas-11`).

## Fase 0: Concepto (`alpha`)

**Contenido.** Especificación conceptual, nombres, licencias, gobierno y este roadmap.

**Estado.** Cerrada con la versión 1.0.0-alpha.2, que cumple los criterios de salida de [Fases](spec/30-proyecto.md#pro-fase).

**Sale cuando** el consejo de mantenedores, hoy formado solo por el editor, declara cerrada la especificación conceptual y se publica la versión de cierre con su etiqueta.

## Fase 1: Definición concreta mínima (`alpha`)

**Decisiones.**

- El asistente de pruebas (`anx-pendiente-14`).
- Cómo se implementa Dintel para que T3 pueda demostrarse: extraído del asistente o verificado contra la semántica mecanizada.

**Primer destino: RISC-V de 64 bits**, en freestanding y en hosted sobre una frontera de llamadas al sistema.

- Su especificación de destino, con la semántica de la arquitectura adoptada por referencia del modelo formal oficial y su modelo de fugas (`dst-spec-14`).
- Una placa física, porque `dst-gobierno-5` exige ejecutar las pruebas de los intrínsecos en hardware real.

**Mecanización.** Semánticas de Stela y de Sillar, ejecutables en el asistente.

**Definiciones concretas, por RFC.**

- La sintaxis de Zea, con su formateador de referencia (`fam-objetivos-15`).
- Las codificaciones y los formatos que necesita la base de confianza: `anx-pendiente-2` a `anx-pendiente-6`.

**Conformidad.** Conjunto de pruebas v0, con la matriz de métodos de verificación de `cnf-pruebas-2`.

**Sale cuando:**

- las semánticas de Stela y de Sillar ejecutan un corpus fijo de programas de referencia;
- la sintaxis de Zea está aprobada y su formateador pasa la prueba de ida y vuelta;
- el conjunto v0 tiene al menos una prueba por cada requisito que se verifica por prueba en la clase Verificador.

## Fase 2: Base de confianza y semilla (`alpha`)

**Componentes.**

- **Semilla:** escrita en otro lenguaje, fuera de la TCB, compila solo Zea y sin optimización.
- **Dintel:** con la comprobación de la evidencia de mutación y el evaluador de contraejemplos.
- **Cincel:** su núcleo.
- **Plomada:** puede funcionar todavía sin pasadas que validar.
- **Chinampa:** las capas core y alloc, y una std mínima (archivos y salida del proceso).
- **Speculum y Estuco:** Speculum mínimo, porque R5 rige desde el primer módulo, y Estuco para Zea.

**Mecanización.** T1 a T4.

**Personas.** Al menos los dos revisores que `dst-gobierno-7` exige para admitir la especificación del primer destino.

**Sale cuando:**

- las pruebas de la clase Verificador pasan, positivas y negativas, incluidas las de cada clase de debilidad, en freestanding y en hosted;
- los binarios se ejecutan en hardware real;
- las atestaciones son idénticas en dos máquinas distintas.

## Fase 3: Auto-hospedaje (`alpha` → `beta.1`)

**Contenido.**

- La cadena de herramientas se reescribe en Zea. Tiene que ser solo en Zea, porque la semilla actúa como cadena independiente de la doble compilación diversa en todas las versiones (`bootstrap-4`).
- Pulido con Plomada, y una primera versión de Glosa.

**Mecanización.** T8 y T9.

**Bootstrap.**

1. **Etapa 1:** la semilla compila la cadena.
2. **Etapa 2:** la etapa 1 compila la cadena.
3. **Etapa 3:** la etapa 2 compila la cadena.

**Sale cuando:**

- la etapa 2 coincide bit a bit con la etapa 3 (la etapa 1 no tiene por qué coincidir, porque la produjo la semilla);
- la doble compilación diversa según `bootstrap-4`, con la semilla como cadena independiente, produce un binario idéntico al de la etapa 3;
- la cadena pasa el conjunto de pruebas en el primer destino, en los tres perfiles.

Ese último evento abre `beta` (`pro-compatibilidad-10`).

## Fase 4: Familia (`beta` → `rc.1`)

**Lenguajes.** Los otros cinco, uno detrás de otro, cada uno con su RFC de sintaxis, su formateador, su frontend y sus pruebas, en este orden:

1. Talud
2. Solsticio
3. Relevo
4. Amate
5. Voluta

**Herramientas y biblioteca.** Speculum y Glosa completos, Chinampa completa en cada perfil, observabilidad e interoperabilidad.

**Segundo destino.** La arquitectura de la máquina de desarrollo (ARM64 o x86-64), con su semántica formal.

**Mecanización.** T5 y T6.

**Sale cuando** el conjunto de pruebas pasa con los seis lenguajes en los tres perfiles, en el sentido de `dst-perfiles-7`. Ese evento abre `rc` (`pro-compatibilidad-10`).

## Fase 5: Ecosistema y 1.0 (`rc` → 1.0.0)

**Contenido.** Ceiba, Pochteca y el tercer destino.

**Mecanización.** T7 en los tres destinos de referencia.

**Auditoría.** Auditoría completa del núcleo de Dintel, con su informe publicado (`dintel-tcb-4`).

**Sale cuando:**

- el conjunto de pruebas pasa en los tres destinos de referencia;
- T1 a T9 están mecanizados;
- el informe de auditoría está publicado;
- el consejo de mantenedores aprueba la 1.0.0.

## Repositorios

| Repositorio           | Se crea al empezar | Contenido                                                       |
|-----------------------|--------------------|-----------------------------------------------------------------|
| `dubito-spec`         | Ya existe          | La especificación y este roadmap.                               |
| `dubito-rfcs`         | Fase 1             | Propuestas de lo concreto.                                      |
| `dubito-mecanizacion` | Fase 1             | Semánticas y teoremas en el asistente de pruebas.               |
| `dubito-rumbo`        | Fase 1             | Especificaciones de destino del proyecto.                       |
| `dubito-conformidad`  | Fase 1             | Conjunto de pruebas de conformidad y su trazabilidad.           |
| `dubito-semilla`      | Fase 2             | El compilador semilla.                                          |
| `dubito`              | Fase 2             | La cadena de herramientas y Chinampa, en un solo repositorio.   |

## Riesgos

| Riesgo                                     | Cómo se cubre                                                                                                                                          |
|--------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| Un solo mantenedor                         | Incorporar al menos dos revisores antes de la fase 2, que `dst-gobierno-7` exige de todos modos.                                                      |
| Costo de la mecanización                   | Adoptar el modelo formal oficial de cada arquitectura, dejar T7 al final y declarar como supuestos los teoremas aún no mecanizados.                  |
| Rendimiento de Dintel y de Plomada         | Cada fase publica los tiempos de verificación y de validación de traducción del corpus de referencia, para detectar a tiempo si se vuelven inviables. |
| Alcance de la 1.0                          | Si hace falta acotarla, los actores remotos, los plugins y el par externo pueden pasar a experimentales según `pro-ciclo-2`.                         |
| Conflictos de marca                        | Búsqueda formal de marcas antes de `beta`.                                                                                                             |
