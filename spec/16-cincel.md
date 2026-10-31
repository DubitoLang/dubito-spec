---
title: "Cincel"
order: 16
mark: cincel
mark_group: plat
---
*Plataforma · backend*

# Cincel

**Rol:** backend · **En la TCB:** sí, su núcleo

Cincel es el backend de la plataforma: talla la representación verificada en código del destino.

## <a id="dst-backend"></a>Responsabilidades

- <a id="dst-backend-1"></a>Baja la representación verificada a la IR de bajo nivel, la optimiza según [Optimización](15-pulido.md#optimizacion) y genera el código del destino, incluido el enlazado final. Su núcleo (la bajada, la selección de instrucciones, la asignación de registros, el enlazado y Plomada, el validador de traducción) pertenece a la TCB; las pasadas de optimización con validación de traducción no. `dst-backend-1`
- <a id="dst-backend-2"></a>Nunca introduce bifurcaciones, accesos indexados por tablas ni operaciones de latencia variable sobre datos secretos, nunca elimina un borrado de secretos y aplica las protecciones de especulación marcadas. Estas propiedades forman parte de su teorema de corrección, y la validación de traducción de cada pasada las comprueba. `dst-backend-2`
- <a id="dst-backend-3"></a>Genera, a partir de los efectos de cada binario, un perfil para el mecanismo de reducción de privilegios del destino, como defensa adicional; la garantía es la estática (R1). `dst-backend-3`
- <a id="dst-backend-4"></a>Puede sustituirse por otro backend conforme sin cambiar los lenguajes. `dst-backend-4`
- <a id="dst-backend-5"></a>La convención de llamada interna no es estable entre versiones; la externa es la de la plataforma. `dst-backend-5`

---

← [Pulido](15-pulido.md) · [Índice](README.md) · [Estuco](17-estuco.md) →
