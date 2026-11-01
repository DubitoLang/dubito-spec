---
title: "Talud"
order: 4
mark: talud
mark_group: lang
---
*Lenguaje orientado a objetos*

# Talud

**Paradigma:** orientado a objetos · **Perfiles:** core, freestanding, hosted

Talud es el lenguaje orientado a objetos de la familia. Agrupa datos, invariante y métodos en clases, admite herencia simple desde clases declaradas abiertas, y liga herencia y contratos: una subclase solo puede prometer más y exigir menos que su base.

## <a id="tal-clasificacion"></a>Clasificación

| Eje                                | Talud                                                                                     |
|------------------------------------|-------------------------------------------------------------------------------------------|
| <a id="tal-clasificacion-1"></a>Paradigma `tal-clasificacion-1`    | Orientado a objetos con clases; imperativo                                                |
| <a id="tal-clasificacion-2"></a>Nivel `tal-clasificacion-2`        | Aplicaciones y bibliotecas de dominio; disponible en freestanding                         |
| <a id="tal-clasificacion-3"></a>Memoria `tal-clasificacion-3`      | Ownership y préstamos; objetos por valor                                                  |
| <a id="tal-clasificacion-4"></a>Evaluación `tal-clasificacion-4`   | Estricta, de izquierda a derecha                                                          |
| <a id="tal-clasificacion-5"></a>Totalidad `tal-clasificacion-5`    | Total por defecto                                                                         |
| <a id="tal-clasificacion-6"></a>Polimorfismo `tal-clasificacion-6` | De subtipo (métodos abiertos), paramétrico y por traits                                   |
| <a id="tal-clasificacion-7"></a>Despacho `tal-clasificacion-7`     | Virtual en métodos abiertos llamados a través de un objeto de clase; estático en el resto |
| <a id="tal-clasificacion-8"></a>Herencia `tal-clasificacion-8`     | Simple, solo desde clases abiertas o abstractas                                           |
| <a id="tal-clasificacion-9"></a>Concurrencia `tal-clasificacion-9` | Concurrencia estructurada; ausencia de carreras por tipos                                 |

## <a id="tal-clases"></a>Clases y objetos

- <a id="tal-clases-1"></a>Una clase declara campos, invariante, inicializadores y métodos. Los campos son privados a la clase y a sus subclases del mismo paquete; un campo público puede leerse desde fuera pero solo se modifica en los métodos de la clase. `tal-clases-1`
- <a id="tal-clases-2"></a>Una clase es final salvo que se declare abierta o abstracta, y un método solo puede redefinirse si se declara abierto. Las clases abstractas no se instancian, y toda subclase concreta define sus métodos abstractos. `tal-clases-2`
- <a id="tal-clases-3"></a>Un valor de una clase es exactamente de esa clase. El polimorfismo de subtipo existe solo a través de objetos de clase, detrás de un préstamo o de un dueño. La conversión hacia la base es explícita, y hacia una subclase devuelve un opcional. `tal-clases-3`
- <a id="tal-clases-4"></a>Los objetos no tienen identidad implícita: se comparan solo si su clase implementa igualdad, y la identidad existe solo para objetos con conteo de referencias. `tal-clases-4`
- <a id="tal-clases-5"></a>Las clases genéricas se monomorfizan. Una clase implementa traits y DEBE definir sus funciones con la regla de refinamiento. `tal-clases-5`

## <a id="tal-construccion"></a>Construcción e invariantes

- <a id="tal-construccion-1"></a>Un inicializador asigna cada campo exactamente una vez antes de terminar; leer un campo no asignado es un error. El de una subclase llama primero a uno de su base. `tal-construccion-1`
- <a id="tal-construccion-2"></a>Un inicializador que puede fallar devuelve un resultado con error; si falla, ningún objeto llega a existir y los campos ya asignados se destruyen. `tal-construccion-2`
- <a id="tal-construccion-3"></a>La invariante vale al terminar cada inicializador y al entrar y salir de cada método público. Mientras un método tiene el objeto prestado de forma exclusiva, no existe otro préstamo, así que nadie lo observa con la invariante rota y la reentrada queda excluida. `tal-construccion-3`

## <a id="tal-herencia"></a>Herencia y redefinición

- <a id="tal-herencia-1"></a>Una clase extiende como máximo una clase abierta o abstracta y hereda sus campos, invariante y métodos. `tal-herencia-1`
- <a id="tal-herencia-2"></a>Una redefinición puede añadir una precondición alternativa (la efectiva es la de la base *o* la nueva, así que solo se debilita) y una postcondición adicional (la efectiva es la de la base *y* la nueva, así que solo se fortalece). `tal-herencia-2`
- <a id="tal-herencia-3"></a>La invariante de una subclase es la conjunción de la suya y la de la base. `tal-herencia-3`
- <a id="tal-herencia-4"></a>Una redefinición no puede declarar efectos que el original no tenga. El verificador genera la VC de refinamiento de cada redefinición. `tal-herencia-4`
- <a id="tal-herencia-5"></a>Un método abierto fija el máximo de efectos de todas sus redefiniciones. `tal-herencia-5`
- <a id="tal-herencia-6"></a>Una clase puede renunciar a ser transferible o compartible. `tal-herencia-6`
- <a id="tal-herencia-7"></a>Las pruebas de una clase abierta se ejecutan sobre cada subclase concreta del paquete. `tal-herencia-7`

## <a id="tal-pendiente"></a>Lo que queda por definir *(Informativa)*

La sintaxis concreta (`anx-pendiente-1`), que se elige según la [elección de la sintaxis](01-familia.md#fam-eleccion), y los nombres de su biblioteca de soporte (`anx-pendiente-7`). Todo está registrado en el [anexo A](33-anexo-a.md).

---

← [Zea](03-zea.md) · [Índice](README.md) · [Solsticio](05-solsticio.md) →
