---
title: "Rumbo"
order: 19
mark: rumbo
mark_group: plat
---
*Plataforma · especificaciones de destino*

# Rumbo

**Rol:** especificaciones de destino · **En la TCB:** sí

Rumbo es el conjunto de especificaciones de destino de la plataforma: cada destino tiene la suya, y en ella se declara todo lo que el destino provee y en qué se confía. Cómo adaptar un destino nuevo está en [Adaptar un destino](26-confianza.md#conf-destinos).

## <a id="dst-spec"></a>Contenido de una especificación

<a id="dst-spec-1"></a>Toda especificación de destino declara: `dst-spec-1`

- <a id="dst-spec-2"></a>Su perfil, su sistema operativo y su [tipo de frontera](26-confianza.md#conf-fronteras). `dst-spec-2`
- <a id="dst-spec-3"></a>Las bases de la biblioteca estándar disponibles y los modos de aislamiento admitidos, con su mecanismo. `dst-spec-3`
- <a id="dst-spec-4"></a>La arquitectura y sus extensiones: las garantizadas y las que pueden detectarse al arrancar. `dst-spec-4`
- <a id="dst-spec-5"></a>El ancho máximo de los atómicos y cómo se implementa el punto flotante, siempre con la semántica de IEEE 754. `dst-spec-5`
- <a id="dst-spec-6"></a>Tamaños, alineación y orden de bytes de los tipos. `dst-spec-6`
- <a id="dst-spec-7"></a>Los intrínsecos, con firma, efectos y contratos, que el verificador asume como axiomas. `dst-spec-7`
- <a id="dst-spec-8"></a>La semántica de aborto y si admite aborto por región. `dst-spec-8`
- <a id="dst-spec-9"></a>La convención de llamada de la plataforma y el formato ejecutable. `dst-spec-9`
- <a id="dst-spec-10"></a>Las operaciones de latencia independiente de los datos, las protecciones de especulación y la protección de memoria con secretos que ofrece. `dst-spec-10`
- <a id="dst-spec-11"></a>Las fronteras asíncronas que provee, con su modelo de fallos. `dst-spec-11`
- <a id="dst-spec-12"></a>El arranque que establece la máquina abstracta antes del primer código del programa. `dst-spec-12`

<a id="dst-spec-13"></a>La especificación crece solo de forma explícita: una operación que no figura en ella no puede usarse, y añadirla es un cambio auditado de la TCB. Su parte de intrínsecos es declarativa (tipos, efectos e intrínsecos con contratos, sin cuerpos) y es el único lugar donde se admiten suposiciones. `dst-spec-13`

<a id="dst-spec-14"></a>Toda especificación de destino de referencia o revisada incluye además la semántica operacional de la arquitectura, en la parte que usa el código que genera el backend, y el modelo de fugas de canal lateral que cubre la disciplina de tiempo constante, ambos mecanizados en el mismo asistente de pruebas que las semánticas de Stela y de Sillar. Si el responsable de la arquitectura publica una semántica formal oficial, se adopta por referencia. Sin esta semántica, T6 y T7 no pueden demostrarse para ese destino y figuran como supuestos en el inventario de confianza. `dst-spec-14`

## <a id="dst-gobierno"></a>Gobierno de las especificaciones

| Nivel                       | Quién la mantiene                               | Uso                                                       |
|-----------------------------|-------------------------------------------------|-----------------------------------------------------------|
| Referencia `dst-gobierno-1` | El proyecto                                     | Destinos de la implementación de referencia               |
| Revisada `dst-gobierno-2`   | Un mantenedor externo, con la revisión de abajo | Publicación en el registro                                |
| Local `dst-gobierno-3`      | Cualquiera, sin revisión                        | Uso privado; queda indicado en el inventario de confianza |

- <a id="dst-gobierno-4"></a>**Trazabilidad.** Cada intrínseco y cada suposición cita la documentación del procesador o del sistema de la que proviene. `dst-gobierno-4`
- <a id="dst-gobierno-5"></a>**Conformidad.** A partir de los contratos de cada intrínseco se generan pruebas que se ejecutan en el hardware y el sistema reales; si alguna falla, la especificación no se admite. `dst-gobierno-5`
- <a id="dst-gobierno-6"></a>**Consistencia.** El verificador intenta demostrar falso a partir de sus axiomas. `dst-gobierno-6`
- <a id="dst-gobierno-7"></a>**Revisión.** Dos revisores independientes la firman. `dst-gobierno-7`
- <a id="dst-gobierno-8"></a>**Mínimo.** Solo se añade un intrínseco que algo necesita; entre versiones menores solo se añaden axiomas. `dst-gobierno-8`
- <a id="dst-gobierno-9"></a>**Erratas.** Un error se publica como aviso sobre la identidad de la especificación, con el efecto descrito en [Compatibilidad](30-proyecto.md#pro-compatibilidad). `dst-gobierno-9`

---

← [Glosa](18-glosa.md) · [Índice](README.md) · [Destinos](20-destinos.md) →
