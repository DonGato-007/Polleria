# Requirements Document

## Introduction

Este documento define los requisitos para mejorar la sección de Menú en index.html con funcionalidades interactivas. El sistema permitirá controlar la velocidad del carrusel de categorías, implementar navegación interactiva mediante categorías (bolitas), y gestionar la visibilidad dinámica de las secciones de productos según la categoría seleccionada.

## Glossary

- **Category_Carousel**: El componente de carrusel horizontal que muestra las categorías de menú (`.categories-scroll` y `.categories-track`)
- **Category_Item**: Cada elemento individual de categoría representado visualmente como una "bolita" con ícono y etiqueta (`.cat-item`)
- **Product_Section**: Cada sección HTML que contiene los productos de una categoría específica (elementos `<section>` con IDs como `sec-brasa`, `sec-mixto`, etc.)
- **Active_Category**: La categoría actualmente seleccionada por el usuario
- **Default_Category**: La categoría "Pollo a la Brasa" que debe estar visible por defecto al cargar la página
- **Animation_Speed**: La duración de la animación CSS `scrollCategories` que controla la velocidad del carrusel

## Requirements

### Requirement 1: Reducir Velocidad del Carrusel de Categorías

**User Story:** Como usuario, quiero que el carrusel de categorías se mueva más lento, para que pueda leer y seleccionar las categorías con mayor facilidad.

#### Acceptance Criteria

1. WHEN la página carga, THE Category_Carousel SHALL tener una Animation_Speed mayor a 25 segundos
2. THE Category_Carousel SHALL mantener el movimiento continuo automático con la nueva velocidad
3. WHEN el usuario posiciona el cursor sobre el carrusel, THE Category_Carousel SHALL pausar la animación
4. WHEN el usuario retira el cursor del carrusel, THE Category_Carousel SHALL reanudar la animación

### Requirement 2: Implementar Visibilidad Dinámica de Secciones de Productos

**User Story:** Como usuario, quiero que solo se muestre la sección de productos de la categoría seleccionada, para que pueda navegar el menú de forma más organizada y enfocada.

#### Acceptance Criteria

1. WHEN la página carga, THE Product_Section correspondiente a Default_Category SHALL estar visible
2. WHEN la página carga, THE Product_Section de todas las categorías excepto Default_Category SHALL estar oculta
3. WHEN el usuario hace clic en un Category_Item, THE Product_Section correspondiente a esa categoría SHALL volverse visible
4. WHEN el usuario hace clic en un Category_Item, THE Product_Section de todas las demás categorías SHALL ocultarse
5. THE Product_Section SHALL aparecer debajo de la sección de categorías (después del elemento `.categories-scroll`)

### Requirement 3: Gestionar Estado Visual de Categoría Activa

**User Story:** Como usuario, quiero ver claramente qué categoría está seleccionada, para que pueda identificar fácilmente la sección de productos que estoy visualizando.

#### Acceptance Criteria

1. WHEN la página carga, THE Category_Item correspondiente a Default_Category SHALL tener la clase CSS `active`
2. WHEN el usuario hace clic en un Category_Item, THE Category_Item seleccionado SHALL recibir la clase CSS `active`
3. WHEN el usuario hace clic en un Category_Item, THE Category_Item previamente activo SHALL perder la clase CSS `active`
4. THE Category_Item con clase `active` SHALL mostrar un borde de color `var(--accent2)` y fondo con transparencia según los estilos CSS existentes

### Requirement 4: Implementar Función de Navegación por Categorías

**User Story:** Como desarrollador, quiero una función JavaScript que gestione la navegación entre categorías, para que el sistema pueda cambiar dinámicamente las secciones visibles.

#### Acceptance Criteria

1. THE System SHALL proporcionar una función JavaScript que acepte un identificador de sección como parámetro
2. WHEN la función es invocada con un identificador de sección válido, THE System SHALL ocultar todas las Product_Section
3. WHEN la función es invocada con un identificador de sección válido, THE System SHALL mostrar únicamente la Product_Section correspondiente al identificador
4. WHEN la función es invocada con un identificador de sección válido, THE System SHALL actualizar el estado visual de los Category_Item para reflejar la selección actual
5. THE System SHALL mantener la funcionalidad existente de scroll suave hacia la sección visible

### Requirement 5: Preservar Funcionalidad Existente del Carrito y Navegación

**User Story:** Como usuario, quiero que todas las funcionalidades existentes del sitio continúen funcionando, para que la nueva interactividad no afecte mi experiencia de compra.

#### Acceptance Criteria

1. WHEN el usuario hace clic en el botón "COMPRAR" de un producto, THE System SHALL agregar el producto al carrito independientemente de la categoría visible
2. WHEN el usuario hace clic en el botón de WhatsApp de un producto, THE System SHALL abrir WhatsApp con el mensaje del producto independientemente de la categoría visible
3. WHEN el usuario navega usando los enlaces del navbar, THE System SHALL mantener el comportamiento de scroll suave existente
4. THE System SHALL mantener la funcionalidad del carrito de compras sin modificaciones
5. THE System SHALL mantener la funcionalidad de los modales y overlays existentes

### Requirement 6: Configurar Categoría por Defecto al Cargar la Página

**User Story:** Como usuario, quiero ver la sección "Pollo a la Brasa" al cargar la página, para que pueda acceder inmediatamente a los productos más populares.

#### Acceptance Criteria

1. WHEN la página termina de cargar, THE System SHALL ejecutar automáticamente la función de navegación con el identificador `sec-brasa`
2. WHEN la página termina de cargar, THE Product_Section con ID `sec-brasa` SHALL estar visible
3. WHEN la página termina de cargar, THE Category_Item correspondiente a "Pollo a la Brasa" SHALL tener la clase `active`
4. THE System SHALL ejecutar esta inicialización después de que el DOM esté completamente cargado

### Requirement 7: Mantener Compatibilidad con Elementos Duplicados del Carrusel

**User Story:** Como desarrollador, quiero que la función de navegación funcione correctamente con los elementos duplicados del carrusel, para que el efecto de bucle infinito se mantenga sin errores.

#### Acceptance Criteria

1. WHEN el usuario hace clic en un Category_Item duplicado (segunda mitad del carrusel), THE System SHALL activar la misma Product_Section que su contraparte original
2. WHEN el usuario hace clic en un Category_Item duplicado, THE System SHALL actualizar el estado `active` tanto del elemento original como del duplicado
3. THE System SHALL identificar elementos duplicados por su identificador de sección asociado, no por su posición en el DOM
4. THE System SHALL mantener sincronizado el estado visual de todos los Category_Item que correspondan a la misma categoría
