---
title: "Dintel"
order: 12
mark: dintel
mark_group: plat
---
*Plataforma · verificador*

# Dintel

**Rol:** verificador · **En la TCB:** sí

Dintel decide si un módulo puede convertirse en código máquina. Revisa la evidencia que el módulo trae en lugar de volver a buscarla, por lo que es un programa pequeño y auditable. No confía en quien produjo la representación intermedia.

## <a id="dintel-pasos"></a>Proceso de verificación

<a id="dintel-pasos-1"></a>Los pasos se ejecutan en orden; el primero que falla detiene la verificación. `dintel-pasos-1`

1.  <a id="dintel-pasos-2"></a>**Forma canónica.** El módulo está en su única representación y cada identidad es correcta. `dintel-pasos-2`
2.  <a id="dintel-pasos-3"></a>**Dependencias.** Cada import existe y tiene atestación válida. `dintel-pasos-3`
3.  <a id="dintel-pasos-4"></a>**Tipos y ownership.** Dueño único, préstamos dentro de su vida, transferibilidad y compartibilidad de lo que cruza entre tareas, pila acotada de cada tarea y ningún valor fantasma en código ejecutable. `dintel-pasos-4`
4.  <a id="dintel-pasos-5"></a>**Efectos y disponibilidad.** Contención en cada llamada; cada intrínseco existe en la especificación del destino; cada extensión del procesador se usa con su testigo; las variantes de un módulo comparten interfaz; en un binario, todo requisito tiene un intrínseco o un proveedor. `dintel-pasos-5`
5.  <a id="dintel-pasos-6"></a>**Procedencia.** Toda conversión ocurre en una justificación; ningún dato secreto determina lo que la disciplina de tiempo constante prohíbe; el análisis especulativo marca dónde aplicar protecciones. `dintel-pasos-6`
6.  <a id="dintel-pasos-7"></a>**Cobertura de VC.** Toda VC y todo contrato tienen evidencia; el grafo de demostraciones es acíclico; toda suposición proviene de la especificación del destino. `dintel-pasos-7`
7.  <a id="dintel-pasos-8"></a>**Evidencia.** Comprueba cada certificado y aplica la política de comprobaciones en ejecución. De la evidencia de mutación de las definiciones nuevas o modificadas comprueba que cada mutante declarado aplica un operador adoptado, que cada mutante eliminado lo está por el contraejemplo que trae, que cada equivalente trae su certificado y que cada postcondición de código ejecutable elimina al menos un mutante (R5). No genera mutantes ni busca contraejemplos. `dintel-pasos-8`
8.  <a id="dintel-pasos-9"></a>**Atestación.** Emite un documento firmado. `dintel-pasos-9`

## <a id="dintel-atestacion"></a>Atestación

<a id="dintel-atestacion-1"></a>Una atestación es un documento firmado y determinista: dos ejecuciones de la misma versión del verificador sobre el mismo módulo producen el mismo documento. Se expresa con el marco de atestaciones in-toto, con la procedencia de compilación de SLSA y un predicado propio para la evidencia; se firma en un sobre DSSE, y sus resúmenes usan SHA-256 (FIPS 180-4). Contiene: `dintel-atestacion-1`

- <a id="dintel-atestacion-2"></a>La identidad del módulo o binario, del verificador, del destino y de cada dependencia con su atestación. `dintel-atestacion-2`
- <a id="dintel-atestacion-3"></a>Las identidades separadas de código, parte fantasma y pruebas. `dintel-atestacion-3`
- <a id="dintel-atestacion-4"></a>El presupuesto del solucionador y de la evaluación en compilación. `dintel-atestacion-4`
- <a id="dintel-atestacion-5"></a>Un resumen de la evidencia por clase y la lista de comprobaciones en ejecución. `dintel-atestacion-5`
- <a id="dintel-atestacion-6"></a>El resultado de la mutación. `dintel-atestacion-6`
- <a id="dintel-atestacion-7"></a>El [inventario de confianza](26-confianza.md#conf-inventario), las desclasificaciones de datos secretos y las protecciones de especulación aplicadas. `dintel-atestacion-7`

**Regla**

<a id="dintel-atestacion-8"></a>El backend solo genera código para un módulo con atestación válida. `dintel-atestacion-8`

## <a id="dintel-tcb"></a>Base de cómputo confiable

| Elemento                                                          | Por qué es de confianza                                                            |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------|
| El verificador, incluido su comprobador de pruebas `dintel-tcb-1` | Decide qué se acepta.                                                              |
| El núcleo del backend, con Plomada `dintel-tcb-2`                 | Traduce la representación verificada a código máquina, incluido el enlazado final, y valida las pasadas que no pertenecen al núcleo. |
| La especificación de cada destino `dintel-tcb-3`                  | Define la semántica de los intrínsecos y del arranque.                             |

<a id="dintel-tcb-4"></a>Los frontends, el solucionador, la herramienta de mutación, las pasadas de Pulido con validación de traducción y cualquier generador de código quedan fuera de la TCB. El verificador sigue el criterio de de Bruijn: su núcleo solo comprueba evidencia (lo que incluye evaluar un contraejemplo con la semántica de Stela, pero nunca buscar pruebas, contraejemplos ni mutantes) y es pequeño: cada versión publica el tamaño de su núcleo y el informe de su auditoría completa; su corrección respecto a la semántica mecanizada se demuestra en el mismo asistente de pruebas. `dintel-tcb-4`

<a id="dintel-tcb-5"></a>La tabla enumera lo que se ejecuta al compilar. La definición completa de la TCB, que incluye además la base de la mecanización y las pasadas sin validación que un binario declare, está en [Capas de confianza](26-confianza.md#conf-capas). `dintel-tcb-5`

## <a id="dintel-rechazos"></a>Motivos de rechazo

<a id="dintel-rechazos-1"></a>Forma no canónica; dependencia sin atestación; violación de ownership; efecto no declarado o intrínseco inexistente; flujo de procedencia no autorizado; VC sin evidencia o refutada; certificado inválido; comprobaciones por encima de la política; valor no transferible cruzando entre tareas; valor fantasma en código ejecutable; implementación que no refina su contrato; requisito sin proveedor; extensión sin testigo; variantes incompatibles; pila no acotable sin cota declarada; declaración nativa mal formada; telemetría con datos excluidos; confianza no admitida por el destino; VC desconocida sin comprobación posible; razonamiento circular; suposición fuera de una especificación de destino; violación de tiempo constante; idempotencia sin demostrar; plugin o par fuera de lo declarado; postcondición que no elimina ningún mutante. `dintel-rechazos-1`

## <a id="dintel-pendiente"></a>Lo que queda por definir *(Informativa)*

El predicado de evidencia de las atestaciones, y el algoritmo de firma y la gestión de claves dentro de DSSE (`anx-pendiente-3`). Todo está registrado en el [anexo A](33-anexo-a.md).

---

← [Sillar](11-sillar.md) · [Índice](README.md) · [Plomada](13-plomada.md) →
