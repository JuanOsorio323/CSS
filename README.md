Catálogo Web - Refactorización con Arquitectura BEM y Modular
Proyecto web desarrollado para la estructuración y refactorización de un catálogo de productos, migrando de un diseño monolítico a una arquitectura modular basada en componentes y siguiendo estrictamente la metodología BEM (Block, Element, Modifier).
Estructura del Proyecto y Directorios
El código fuente organiza los estilos de manera modular y estructurada dentro de la carpeta `css/`, separando los componentes visuales de las plantillas globales (layout) según los requerimientos técnicos del proyecto:
```text
catalogo/
├── css/
│   ├── components/
│   │   ├── template/
│   │   │   ├── footer.css       # Módulo estructural del pie de página
│   │   │   └── header.css       # Módulo estructural de la cabecera y banner
│   │   ├── base.css             # Estilos globales, reseteo y configuración base
│   │   ├── sidebar.css          # Módulo de filtros y navegación lateral
│   │   └── tarjeta.css          # Módulo de presentación de productos (Tarjetas)
│   └── styles.css               # Hoja de estilos maestra (Variables :root y directivas @import)
├── index.html                   # Punto de entrada principal (Estructura semántica)
├── sapo.jpeg                    # Recurso multimedia y banner principal
└── README.md                    # Documentación técnica del proyecto
```
Decisiones Técnicas y Metodológicas
Metodología BEM (Block, Element, Modifier): Implementación de convenciones estrictas en los selectores CSS (ej. `.tarjeta`, `.tarjeta__titulo`, `.tarjeta__etiqueta--oferta`) para evitar colisiones de nombres, mantener una especificidad plana y facilitar el mantenimiento del código.
Arquitectura Modular (`@import` centralizado): División del archivo monolítico original en módulos independientes por responsabilidad. El archivo maestro `styles.css` concentra la tokenización de variables globales en `:root` (paleta de colores, tipografías y espaciados) y enlaza de forma ordenada cada submódulo ubicado en `components/` y la subcarpeta `template/`.
Separación de Plantillas (`template/`): Agrupación de los elementos estructurales fijos de la interfaz (`header.css` y `footer.css`) dentro de una subcarpeta dedicada, diferenciándolos de los módulos de contenido reutilizables (`tarjeta.css` y `sidebar.css`).
Control de Versiones Atómico (Git): Gestión del repositorio mediante ramas de características (`feature/arquitectura-bem`) y commits estructurados bajo convenciones estándar (`refactor`, `feat`, `docs`), registrando de forma trazable la evolución de la estructura de carpetas y estilos.
