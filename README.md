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

   ## Hallazgos: Centralización de Identidad Visual y Espaciado

1. **La lista completa de variables declaradas (colores y espaciados):**
   - **Variables de Color:**
     - `--primary-color`: `rgb(50, 205, 104)` (Color corporativo principal para encabezados, barras laterales y pie de página).
     - `--secondary-color`: `aquamarine` (Color de fondo global del cuerpo de la página).
     - `--background-color`: `#f8fafc` (Fondo general complementario).
     - `--text-color`: `#333333` (Color base para la tipografía general).
     - `--white-color`: `#ffffff` (Color de fondo para las tarjetas de productos `<article>`).
     - `--link-color`: `#0056b3` (Color principal para enlaces y botones de compra).
     - `--secondary-link-color`: `#2e7d32` (Color para enlaces en la barra lateral).
     - `--footer-link-color`: `#757575` (Color para enlaces del pie de página).
     - `--accent-color`: `#d32f2f` (Color de realce/destacado para el primer producto ID).
   - **Variables de Tipografía:**
     - `--main-font`: `'Poppins', sans-serif` (Tipografía principal importada desde Google Fonts).
   - **Variables de Espaciado (Tokens de Box Model):**
     - `--spacing-small`: `8px` (Espaciado micro).
     - `--spacing-medium`: `15px` (Espaciado estándar para márgenes).
     - `--spacing-large`: `20px` (Espaciado amplio para rellenos/paddings).

2. **La ventaja de reutilizar medidas de margen y relleno en lugar de inventar valores en cada selector:**
   - Permite garantizar una consistencia visual rigurosa en todo el diseño web, logrando proporciones de aire idénticas y armónicas en todas las tarjetas de productos y secciones. Además, previene el error humano de escribir valores aleatorios y agiliza cualquier cambio futuro, ya que si decides modificar el tamaño del espacio, solo debes cambiarlo una sola vez en el `:root`.

3. **De qué manera la centralización en `:root` previene colisiones visuales a medida que la hoja de estilos crece:**
   - Al depender de una única "fuente de verdad" ubicada en el bloque `:root`, cualquier modificación o escalabilidad del diseño se propaga de manera uniforme a todo el documento. Esto elimina el riesgo de discrepancias en los márgenes entre elementos hermanos, previene desajustes estructurales en las cajas y evita que la hoja de estilos se vuelva caótica o difícil de mantener a medida que el proyecto de desarrollo crece.