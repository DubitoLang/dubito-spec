---
title: "Pochteca"
order: 29
mark: pochteca
mark_group: eco
---
*Ecosistema · registro*

# Pochteca

**Rol:** registro de paquetes · **Direccionamiento:** por contenido

Pochteca es el registro público de paquetes de la familia. Almacena las fuentes de cada paquete y sus atestaciones, direccionadas por contenido, y mantiene un registro de transparencia de todo lo publicado. Cualquier registro privado que siga el mismo modelo es intercambiable con él.

## <a id="pochteca-modelo"></a>Modelo

- <a id="pochteca-modelo-1"></a>**Contenido inmutable.** Un módulo publicado nunca cambia ni se borra. Una versión puede retirarse, lo que impide nuevas resoluciones sin romper bloqueos existentes. `pochteca-modelo-1`
- <a id="pochteca-modelo-2"></a>**Espacios de nombres** por organización, con propiedad ligada a identidades verificadas y sin claves de larga duración; las transferencias de propiedad quedan registradas. `pochteca-modelo-2`
- <a id="pochteca-modelo-3"></a>**Protección de nombres.** Los nombres nuevos confundibles con uno existente, según la detección de confundibles de UTS \#39, requieren revisión. `pochteca-modelo-3`
- <a id="pochteca-modelo-4"></a>**Registro de transparencia** de solo anexado y auditable, con pruebas de inclusión y de consistencia según RFC 9162: publicaciones, retiradas, avisos y transferencias son entradas, y nada se borra. `pochteca-modelo-4`
- <a id="pochteca-modelo-5"></a>**Metadatos firmados** según The Update Framework (TUF), con roles separados y caducidad, para resistir el compromiso del registro, los ataques de repetición y la congelación. `pochteca-modelo-5`
- <a id="pochteca-modelo-6"></a>**Avisos de seguridad** en el formato OSV y exportables como CSAF 2.0 (OASIS). `pochteca-modelo-6`
- <a id="pochteca-modelo-7"></a>**Identificadores** de paquete como Package URL (ECMA-427) y licencias como expresiones SPDX. `pochteca-modelo-7`
- <a id="pochteca-modelo-8"></a>**Distribución por fuentes.** El registro distribuye fuentes y atestaciones, nunca la representación intermedia. Cada cliente regenera los módulos localmente, y como la compilación es reproducible obtiene la misma identidad que figura en la atestación. Así ningún paquete distribuye código de la biblioteca estándar en forma intermedia. `pochteca-modelo-8`
- <a id="pochteca-modelo-9"></a>**Publicación.** El registro reconstruye los módulos desde las fuentes con la cadena fijada y exige la misma identidad, vuelve a ejecutar el verificador, comprueba el incremento de versión y la protección de nombres, y añade la entrada. `pochteca-modelo-9`
- <a id="pochteca-modelo-10"></a>**Verificación del cliente.** El cliente comprueba la identidad de cada contenido, su inclusión en el registro y la consistencia del registro con la última vista, lo que detecta historias distintas para clientes distintos. Por eso ni el registro ni sus espejos están en la TCB: pueden negarse a servir, pero no servir algo distinto sin que se detecte. `pochteca-modelo-10`

---

← [Ceiba](28-ceiba.md) · [Índice](README.md) · [Proyecto e identidad](30-proyecto.md) →
