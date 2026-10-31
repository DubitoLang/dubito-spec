---
title: "Sillar"
order: 11
mark: sillar
mark_group: plat
---
*Plataforma · IR de bajo nivel*

# Sillar

**Rol:** IR de bajo nivel · **Existe:** solo en compilación

Sillar es la representación de bajo nivel entre Stela verificada y el código del destino. Cincel la produce al bajar Stela, Pulido la optimiza y Plomada valida cada transformación.

## <a id="sillar-forma"></a>Forma

- <a id="sillar-forma-1"></a>Código de tres direcciones en forma de asignación única estática (SSA). `sillar-forma-1`
- <a id="sillar-forma-2"></a>Usa los tipos de máquina y el modelo de memoria del destino que declara su especificación ([Rumbo](19-rumbo.md)). `sillar-forma-2`
- <a id="sillar-forma-3"></a>Existe solo en compilación (R3): nunca se distribuye ni se ejecuta. `sillar-forma-3`

## <a id="sillar-anotaciones"></a>Anotaciones obligatorias

<a id="sillar-anotaciones-1"></a>Sillar conserva como anotaciones explícitas todo lo que una optimización DEBE respetar: `sillar-anotaciones-1`

- <a id="sillar-anotaciones-2"></a>los datos secretos y la disciplina de tiempo constante; `sillar-anotaciones-2`
- <a id="sillar-anotaciones-3"></a>las protecciones de especulación; `sillar-anotaciones-3`
- <a id="sillar-anotaciones-4"></a>los borrados de secretos; `sillar-anotaciones-4`
- <a id="sillar-anotaciones-5"></a>los puntos de telemetría; `sillar-anotaciones-5`
- <a id="sillar-anotaciones-6"></a>los límites de los efectos. `sillar-anotaciones-6`

## <a id="sillar-concreto"></a>Lo que queda por definir

<a id="sillar-concreto-1"></a>Su codificación concreta se define en la etapa siguiente, sin contradecir estos requisitos ([anexo A](33-anexo-a.md)). `sillar-concreto-1`

---

← [Stela](10-stela.md) · [Índice](README.md) · [Dintel](12-dintel.md) →
