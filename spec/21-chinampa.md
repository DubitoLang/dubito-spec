---
title: "Chinampa"
order: 21
mark: libs
mark_group: plat
---
*Plataforma · biblioteca estándar*

# Chinampa

**Rol:** biblioteca estándar · **En la TCB:** no; se verifica como cualquier código

Chinampa, la biblioteca estándar, se divide en tres capas según lo que exige del destino. Se verifica como cualquier código y la usan los seis lenguajes. Añade capacidades, nunca garantías (R4). Su contenido concreto no se define en esta fase y está registrado como pendiente en el [anexo A](33-anexo-a.md#anx-pendiente); aquí se fija solo lo que el lenguaje requiere de ella.

## <a id="std-capas"></a>Capas

| Capa                | Requiere                         | Disponible en                      |
|---------------------|----------------------------------|------------------------------------|
| <a id="std-capas-1"></a>core `std-capas-1`  | Nada                             | Todos los destinos                 |
| <a id="std-capas-2"></a>alloc `std-capas-2` | Un proveedor de memoria dinámica | Hosted; freestanding con proveedor |
| <a id="std-capas-3"></a>std `std-capas-3`   | Un destino hosted                | Hosted                             |

## <a id="std-requerido"></a>Lo que el lenguaje requiere

- <a id="std-requerido-1"></a>De **core**: las operaciones numéricas y los modos de redondeo; los traits de igualdad, orden, hash, representación textual, codificación y decodificación; opcionales, resultados y errores acumulativos; iteración con medida de terminación; texto validado; los traits de los proveedores, ámbitos, tareas, cancelación e instantes; atómicos y secciones críticas; testigos de capacidad y su detección; las operaciones de tiempo constante; las fronteras asíncronas y sus transformadores; la carga de plugins; los tipos matemáticos, funciones fantasma y lemas de uso común, incluidos el modelo de error de redondeo y los estados tras una caída. `std-requerido-1`
- <a id="std-requerido-2"></a>De **alloc**: cajas, conteo de referencias con enlaces débiles, colecciones, texto dinámico y datos de forma desconocida. `std-requerido-2`
- <a id="std-requerido-3"></a>De **std**: proveedores predeterminados para hosted, motores de E/S (al menos uno simulado y determinista) y el anfitrión de aislamiento de código nativo. `std-requerido-3`

## <a id="std-bases"></a>Bases de std

<a id="std-bases-1"></a>En hosted, std puede apoyarse en las llamadas al sistema o en la biblioteca que el sistema declara como su interfaz estable. Ambas exponen la misma interfaz con los mismos contratos: cambiar de base no cambia el programa, solo su inventario de confianza. Donde existen las dos, la predeterminada es la de llamadas al sistema, porque confía en menos. En la base del sistema, cada función usada se declara en la especificación del destino, lo que no puede especificarse con precisión llega como *external*, y lo que depende de configuración externa se ejecuta aislado. `std-bases-1`

## <a id="std-portable"></a>Portabilidad

- <a id="std-portable-1"></a>La interfaz portable de std solo incluye operaciones con la misma semántica en todos los sistemas hosted, con contratos idénticos, y se implementa como variantes por destino. `std-portable-1`
- <a id="std-portable-2"></a>Lo que solo existe en un sistema vive aparte y solo puede importarse al compilar para ese sistema. `std-portable-2`
- <a id="std-portable-3"></a>Un error que un sistema puede producir y otro no es una categoría del error común en todos; nunca cambia una firma según el destino. `std-portable-3`
- <a id="std-portable-4"></a>Cada operación de std desciende a un intrínseco del destino; los nombres concretos de cada sistema viven solo en su especificación. `std-portable-4`

**Regla**

<a id="std-portable-5"></a>Ninguna capa usa una operación que no exista en el lenguaje o en la especificación del destino, y ninguna contiene código no verificado (R8, R9). `std-portable-5`

## <a id="std-pendiente"></a>Lo que queda por definir *(Informativa)*

Los módulos, nombres y firmas de las tres capas (`anx-pendiente-7`). Todo está registrado en el [anexo A](33-anexo-a.md).

---

← [Destinos y perfiles](20-destinos.md) · [Índice](README.md) · [Errores y aborto](22-errores.md) →
