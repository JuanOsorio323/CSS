## Cálculo Completo de Puntos de Especificidad
La especificidad determina qué regla CSS gana y se aplica cuando existen colisiones visuales en un elemento. Su jerarquía de puntaje se calcula sumando el valor de cada selector:
* **Etiquetas / Elementos** (`div`, `p`, `a`, `h2`, `ul`, `li`, `header`, `footer`, `main`, `aside`): **1 punto** cada una.
* **Clases** (`.class`) y pseudo-clases (`:hover`): **10 puntos** cada una.
* **Identificadores** (`#id`): **100 puntos** cada uno.

### Desglose y Cálculo de cada Selector Utilizado en el Proyecto:

1. **Selectores de Zona (Aislamiento de Menús):**
   * `header nav ul li a` $\rightarrow$ 4 etiquetas (`nav`, `ul`, `li`, `a`) = **4 puntos** (1 + 1 + 1 + 1)
   * `aside ul li a` $\rightarrow$ 3 etiquetas (`ul`, `li`, `a`) = **3 puntos** (1 + 1 + 1)
   * `footer ul li a` $\rightarrow$ 3 etiquetas (`ul`, `li`, `a`) = **3 puntos** (1 + 1 + 1)

2. **Selectores del Cuerpo Principal (Main):**
   * `main section article a` $\rightarrow$ 3 etiquetas (`section`, `article`, `a`) = **3 puntos** (1 + 1 + 1)
   * `main section article a.btn-comprar` $\rightarrow$ 3 etiquetas (`section`, `article`, `a`) + 1 clase (`.btn-comprar`) = **13 puntos** (1 + 1 + 1 + 10)
   * `main section article a#btn-destacado` $\rightarrow$ 3 etiquetas (`section`, `article`, `a`) + 1 ID (`#btn-destacado`) = **103 puntos** (1 + 1 + 1 + 100)

3. **Pseudo-clases:**
   * `a:hover` $\rightarrow$ 1 etiqueta (`a`) + 1 pseudo-clase (`:hover`) = **11 puntos** (1 + 10)