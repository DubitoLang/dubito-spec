---
title: "Anexo A"
order: 33
---
*Referencia · anexo A*

# Definido por el destino o la implementación

Dubito no tiene comportamiento indefinido: todo programa aceptado tiene un único significado. Lo que esta especificación no fija lo decide el destino o la implementación, y cada punto está enumerado aquí, como exige R9.

## <a id="anx-reglas"></a>Reglas

- <a id="anx-reglas-1"></a>Lo definido por el destino lo DEBE declarar su especificación de destino (Rumbo). `anx-reglas-1`
- <a id="anx-reglas-2"></a>Lo definido por la implementación lo DEBE documentar la declaración de conformidad del producto. `anx-reglas-2`
- <a id="anx-reglas-3"></a>Todo punto que afecta a un binario DEBE quedar registrado en su atestación. `anx-reglas-3`
- <a id="anx-reglas-4"></a>Ningún punto de este anexo puede cambiar el significado de un programa aceptado respecto de la semántica de Stela; solo puede hacer que un programa se acepte o se rechace para un destino. `anx-reglas-4`

## <a id="anx-destino"></a>Definido por el destino

| Punto                                                                                        | Dónde se define en esta especificación                                                             |
|----------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| Perfil, sistema operativo y tipo de frontera del sistema `anx-destino-1`                     | [Rumbo](19-rumbo.md)                                                                               |
| Tamaño y alineación de los tipos de máquina; ancho máximo de los atómicos `anx-destino-2`    | [Concurrencia por perfil](20-destinos.md#dst-concurrencia)                                         |
| Intrínsecos, arranque y forma de reportar el aborto `anx-destino-3`                          | [Rumbo](19-rumbo.md)                                                                               |
| Extensiones del procesador garantizadas y opcionales `anx-destino-4`                         | [Destinos](20-destinos.md)                                                                         |
| Convención de llamada externa `anx-destino-5`                                                | [Cincel](16-cincel.md)                                                                             |
| Modos de aislamiento disponibles y base de std `anx-destino-6`                               | [Modos de aislamiento](26-confianza.md#conf-aislamiento); [Bases de std](21-chinampa.md#std-bases) |
| Modelo de fugas de canal lateral que cubre la disciplina de tiempo constante `anx-destino-7` | [Procedencia](02-nucleo.md#nuc-procedencia)                                                        |

## <a id="anx-implementacion"></a>Definido por la implementación

| Punto                                                                                                                                                                            | Dónde se define en esta especificación                   |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------|
| Sintaxis concreta de cada lenguaje, hasta que se apruebe `anx-implementacion-1`                                                                                                  | [Elección de la sintaxis](01-familia.md#fam-eleccion)    |
| Codificación de Stela y de Sillar (textual o binaria) y formatos propios aún no fijados `anx-implementacion-2`                                                                                       | [Niveles de representación](09-compilador.md#niveles)    |
| Solucionador usado y valor del presupuesto del solucionador `anx-implementacion-3`                                                                                               | [Fases](09-compilador.md#fases)                          |
| Selección de mutantes dentro de los operadores adoptados `anx-implementacion-4`                                                                                                  | [Speculum](14-speculum.md)                               |
| Pasadas de cada perfil de optimización `anx-implementacion-5`                                                                                                                    | [Perfiles de optimización](15-pulido.md#perfiles-opt)    |
| Motores y proveedores predeterminados que ofrece `anx-implementacion-6`                                                                                                          | [Motores](23-es.md#es-motor)                             |
| Texto de los diagnósticos `anx-implementacion-7`                                                                                                                                 | [Diagnósticos y editores](09-compilador.md#diagnosticos) |
| Límites de traducción: anidamiento, tamaño de módulo y número de declaraciones; cada implementación los documenta y un programa que los excede se rechaza `anx-implementacion-8` | [Conformidad](31-conformidad.md)                         |

---

← [Estándares adoptados](32-estandares.md) · [Índice](README.md) · [Fundamentos de diseño](34-fundamentos.md) →
