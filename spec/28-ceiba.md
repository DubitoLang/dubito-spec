---
title: "Ceiba"
order: 28
mark: ceiba
mark_group: eco
---
*Ecosistema · paquetes*

# Ceiba

**Rol:** gestor de paquetes · **En la TCB:** no

Ceiba resuelve, obtiene y verifica dependencias. Una dependencia queda fijada por la identidad de su contenido, no por un número de versión, así que lo que se compila es exactamente lo que se revisó.

## <a id="ceiba-manifiesto"></a>Manifiesto y bloqueo

<a id="ceiba-manifiesto-1"></a>Cada paquete declara en un manifiesto su nombre, su versión, su edición, los destinos que afirma, sus dependencias, la configuración de su binario (proveedores, base, puntos de extensión, pares aceptados) y su política (puntuación mínima de mutación, comprobaciones en ejecución admitidas, presupuestos, etiquetas sensibles, aislamiento). El resultado de la resolución se guarda como un bloqueo que fija cada dependencia por la identidad de su módulo, de su atestación y de su destino. `ceiba-manifiesto-1`

## <a id="ceiba-resolucion"></a>Resolución de versiones

<a id="ceiba-resolucion-1"></a>Resolver versiones con rangos arbitrarios, límites superiores y exclusiones es un problema NP-completo. Ceiba usa selección de versión mínima (Cox, 2018): `ceiba-resolucion-1`

- <a id="ceiba-resolucion-2"></a>**Requisitos.** Solo mínimos dentro de una versión mayor; sin límites superiores, exclusiones ni características opcionales. Lo único que varía la compilación es el destino. `ceiba-resolucion-2`
- <a id="ceiba-resolucion-3"></a>**Selección.** Para cada paquete y versión mayor, el mayor de los mínimos que pide el grafo. Recorre el grafo una vez, es determinista y no busca. `ceiba-resolucion-3`
- <a id="ceiba-resolucion-4"></a>**Estabilidad.** Publicar una versión nueva de una dependencia no cambia ninguna resolución existente; solo una actualización explícita sube los mínimos. `ceiba-resolucion-4`
- <a id="ceiba-resolucion-5"></a>**Versiones mayores distintas** son paquetes distintos y pueden coexistir; sus tipos no se convierten implícitamente. `ceiba-resolucion-5`
- <a id="ceiba-resolucion-6"></a>**Retiradas y avisos.** Una versión retirada nunca se elige para una resolución nueva. Una versión con aviso de seguridad hace fallar la verificación hasta que se actualiza o el paquete raíz reconoce el aviso, que entonces figura en el inventario de confianza. `ceiba-resolucion-6`
- <a id="ceiba-resolucion-7"></a>**Sustitución.** El paquete raíz puede sustituir una dependencia por una copia local que refine su interfaz; se verifica como cualquier código y aparece en el diff de significado. `ceiba-resolucion-7`

## <a id="ceiba-reglas"></a>Reglas

- <a id="ceiba-reglas-1"></a>Una dependencia se obtiene como fuentes y se acepta solo si el módulo regenerado localmente tiene la identidad que figura en una atestación válida para la especificación de destino en uso. `ceiba-reglas-1`
- <a id="ceiba-reglas-2"></a>La instalación no ejecuta código de terceros. `ceiba-reglas-2`
- <a id="ceiba-reglas-3"></a>Los destinos que un paquete afirma se verifican: se rechaza la publicación si algún requisito abierto no puede satisfacerse en un destino declarado. `ceiba-reglas-3`
- <a id="ceiba-reglas-4"></a>Los efectos y el inventario de confianza de una dependencia forman parte de su interfaz; una actualización muestra su diff de significado y el cambio en su inventario. `ceiba-reglas-4`
- <a id="ceiba-reglas-5"></a>El grafo de dependencias de un binario, con su inventario de confianza, se exporta como lista de materiales de software en SPDX 3.0 y en CycloneDX (ECMA-424). `ceiba-reglas-5`

## <a id="ceiba-pendiente"></a>Lo que queda por definir *(Informativa)*

El formato del manifiesto y del archivo de bloqueo (`anx-pendiente-10`) y la forma en que un paquete declara su edición (`anx-pendiente-15`). Todo está registrado en el [anexo A](33-anexo-a.md).

---

← [Modelo de amenazas](27-amenazas.md) · [Índice](README.md) · [Pochteca](29-pochteca.md) →
