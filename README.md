## Hallazgos: Arquitectura Total con Flexbox

### 1. Control del pie de página con `min-height: 100vh` y `flex-direction: column`
Aplicar `min-height: 100vh` junto con `display: flex` y `flex-direction: column` en `.app-layout` fue clave para que la estructura ocupe como mínimo todo el alto visible de la ventana y se organice en un eje vertical (`header`, `.main-wrapper` con `flex: 1` y `footer`). Gracias a ello, si el catálogo tiene pocos productos o la pantalla es alta, `.main-wrapper` absorbe el espacio sobrante y el `<footer>` se mantiene ubicado al final de la página sin quedar flotando a mitad de pantalla, permitiendo a la vez que la página crezca con normalidad si el contenido supera el `100vh`.

### 2. Reemplazo de márgenes laterales por `gap` en los menús de navegación
En lugar de depender de márgenes horizontales en cada enlace (como `margin-right` o `margin-left`, que suelen generar espacios sobrantes en el primer o último ítem o exigir reglas extra para quitarlos), usar `gap: var(--espaciado-medio)` directamente sobre el contenedor flexible de navegación (`header nav ul` / `.nav__list` y `footer ul`) define una separación uniforme únicamente entre elementos adyacentes. Esto hace el código más limpio, evita desajustes al envolver líneas y centraliza el espaciado desde una *custom property*.

### 3. Tarjetas resistentes a distintas longitudes de texto mediante BEM, Custom Properties y Flexbox
Combinar **BEM**, **Custom Properties** y **Flexbox** permitió construir tarjetas (`.card`) estables sin importar si una descripción es corta o extensa:
* **Flexbox** organiza cada tarjeta en columna (`display: flex; flex-direction: column; height: 100%;`), mientras `.card__description` crece con `flex-grow: 1` para actuar como resorte y empujar el precio y `.card__button` hacia la parte inferior, logrando que las acciones queden alineadas entre tarjetas vecinas.
* **BEM** separa con claridad el bloque (`.card`), sus elementos (`.card__title`, `.card__description`, `.card__price`, `.card__button`) y variantes como `.card--destacado` (con su etiqueta mediante `::after`), evitando colisiones de estilos.
* **Custom Properties** (`--espaciado-*`, `--color-*`, `--fuente-principal`) mantienen coherentes los espaciados, bordes y colores en toda la tarjeta y en el resto del sistema.