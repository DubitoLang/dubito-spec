---
title: "Plomada"
order: 13
mark: plomada
mark_group: plat
---
*Plataforma · validador de traducción*

# Plomada

**Rol:** validación de traducción · **En la TCB:** sí

Plomada comprueba, en cada compilación, que la salida de cada pasada de optimización sobre Sillar conserva el significado de su entrada. Gracias a ella, las pasadas de Pulido quedan fuera de la TCB. Las transformaciones del núcleo de Cincel (bajada, selección de instrucciones, asignación de registros y enlazado) no pasan por Plomada: pertenecen a la TCB y su corrección es T7.

## <a id="plomada-proceso"></a>Proceso

- <a id="plomada-proceso-1"></a>Cada pasada validada produce, junto con su salida, un testigo de la correspondencia entre su entrada y su salida. `plomada-proceso-1`
- <a id="plomada-proceso-2"></a>Plomada comprueba el testigo. Si la comprobación falla, la compilación se detiene y no se genera el binario. `plomada-proceso-2`
- <a id="plomada-proceso-3"></a>La comprobación cubre lo que T8 exige preservar: la semántica, incluidos los efectos y su orden, el tiempo constante, las protecciones de especulación, los borrados de secretos y los puntos de telemetría. `plomada-proceso-3`
- <a id="plomada-proceso-4"></a>La comprobación es determinista y su resultado queda registrado en la atestación del binario. `plomada-proceso-4`

## <a id="plomada-tcb"></a>Lugar en la TCB

- <a id="plomada-tcb-1"></a>Plomada pertenece a la TCB junto con el núcleo de [Cincel](16-cincel.md); su corrección es el teorema T8. `plomada-tcb-1`
- <a id="plomada-tcb-2"></a>Una pasada sin validación no pasa por Plomada: pertenece a la TCB y aparece en el inventario de confianza de cada binario que la usa (R9). `plomada-tcb-2`

## <a id="plomada-pendiente"></a>Lo que queda por definir *(Informativa)*

El formato del testigo que comprueba Plomada (`anx-pendiente-4`). Todo está registrado en el [anexo A](33-anexo-a.md).

---

← [Dintel](12-dintel.md) · [Índice](README.md) · [Speculum](14-speculum.md) →
