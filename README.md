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
   
   ## Hallazgos: El Modelo de Caja

1. **La diferencia práctica entre Margin y Padding:**
   - **Padding (Relleno):** Es el espacio interno que se genera entre el contenido real de la caja (textos, imágenes, enlaces) y su borde. Actúa como un colchón por dentro para evitar que los elementos colisionen o toquen los límites de su propio contenedor.
   - **Margin (Margen):** Es el espacio externo que rodea la caja. Su función principal es separar el elemento de otros elementos vecinos o hermanos en la pantalla, evitando que se peguen o colisionen visualmente.

2. **Por qué es obligatorio usar `box-sizing: border-box`:**
   - Por defecto, el navegador calcula el ancho total de un elemento sumando el contenido más el relleno y los bordes por separado (`content-box`), lo que provoca que las cajas crezcan más de lo esperado y rompan la estructura del diseño. Al configurar `box-sizing: border-box;`, le indicamos al navegador que los rellenos y los bordes se calculen *hacia adentro*, garantizando que el tamaño total de la caja se mantenga fiel y exacto a las dimensiones que programamos.

3. **Cómo se ven afectados los elementos hermanos cuando le aplicas un margen grande a uno de ellos:**
   - Los elementos hermanos se desplazan y se alejan de forma proporcional según el espacio exterior que impone ese margen. Además, en el eje vertical (arriba y abajo), si dos elementos hermanos tienen márgenes contiguos, estos pueden fusionarse en un fenómeno conocido como *margin collapsing* (colapso de márgenes), donde el navegador aplica el valor del margen más grande en lugar de sumar ambos, lo cual es fundamental tener en cuenta para calcular espacios exactos en la interfaz.