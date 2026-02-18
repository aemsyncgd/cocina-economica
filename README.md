# 🍳 Cocina Económica (Chef VZLA Pro)

**Cocina Económica** es una aplicación web inteligente diseñada para optimizar la gestión de tu despensa y la planificación de comidas. No es solo un inventario; es un asistente culinario que te ayuda a descubrir qué cocinar basándose en lo que ya tienes, ajustando porciones y ofreciendo consejos diarios para ahorrar tiempo y dinero.

---

## ✨ Características Principales

-   **📦 Gestión de Despensa:** Registra tus ingredientes, cantidades y unidades. La app guarda automáticamente tu inventario en el almacenamiento local.
-   **🔍 Buscador Inteligente:** Busca recetas por **Nombre del Platillo** o por **Ingrediente base**.
-   **🌐 Consulta en la Nube:** Simulación de búsqueda web para encontrar nuevas recetas dinámicamente y añadirlas a tu recetario personal.
-   **⚖️ Control de Stock:** Visualiza instantáneamente qué recetas puedes cocinar hoy con indicadores de color (Verde: Todo listo | Naranja: Falta stock).
-   **🍽️ Porciones Dinámicas:** Ajusta el número de adultos y niños; la app recalcula automáticamente las cantidades de ingredientes necesarias.
-   **📖 Recetario Detallado:** Incluye descripciones, lista de ingredientes calculados y pasos de preparación profesionales.
-   **💡 Tips del Día:** Banner superior con consejos rotativos sobre ahorro y buen manejo de alimentos.
-   **📺 Enlace a YouTube:** Acceso directo a vídeos paso a paso para cada receta.

---

## 🛠️ Stack Tecnológico

La aplicación está construida con tecnologías modernas y ligeras, enfocadas en un rendimiento excepcional y una interfaz reactiva:

-   **HTML5 / Semántica:** Estructura web estándar y accesible.
-   **Tailwind CSS:** Framework de diseño para una interfaz moderna y "premium".
-   **Alpine.js:** El motor de reactividad que gestiona el estado de la aplicación sin sobrecargar el código.
-   **Font Awesome:** Iconografía profesional para una mejor experiencia de usuario.
-   **Vanilla CSS:** Estilos personalizados para efectos de desenfoque (backdrop-filter) y gradientes complejos.

---

## 🎨 Diseño y Paleta de Colores

Se ha seleccionado una paleta inspirada en la frescura de los ingredientes naturales y la limpieza de una cocina moderna:

| Color | Hex | Uso |
| :--- | :--- | :--- |
| **Primary Green** | `#3D7A55` | Acentos principales, botones y estados de éxito. |
| **Dark Green** | `#14201D` | Textos de alto contraste y fondos oscuros. |
| **Pale Mint** | `#DDF6F1` | Fondo general de la aplicación. |
| **Accent Orange** | `#F97316` | Alertas, indicadores de stock faltante y destacados. |
| **Modern Blue** | `#3B82F6` | Botones de consulta web y elementos de ayuda. |

---

## 💻 Arquitectura del Código

### Reactividad con Alpine.js
La lógica principal reside en un objeto dinámico que gestiona el inventario y el recetario en tiempo real:

```javascript
// Muestra de la lógica de inicialización y sincronización
function app() {
    return {
        inventario: JSON.parse(localStorage.getItem('chefvzla_stock')) || [...],
        recetario: JSON.parse(localStorage.getItem('chefvzla_recipes')) || [],
        
        init() {
            // Sincronización persistente con LocalStorage
            this.$watch('inventario', v => localStorage.setItem('chefvzla_stock', JSON.stringify(v)));
            this.$watch('recetario', v => localStorage.setItem('chefvzla_recipes', JSON.stringify(v)));
        },
        
        verificarStock(r) {
            // Lógica inteligente de cruce de datos
            return Object.entries(r.ingredientes).every(([ing, cant]) => {
                const item = this.inventario.find(i => i.nombre.toLowerCase().includes(ing.toLowerCase()));
                return item && item.cantidad >= this.calcularCantidad(cant);
            });
        }
    }
}
```

### Estilos Personalizados
Uso de variables CSS para facilitar cambios de tema y mantenimiento:

```css
:root {
    --primary: #3D7A55;
    --dark: #14201D;
    --bg-light: #DDF6F1;
    --accent-orange: #F97316;
}

.tips-banner {
    background: linear-gradient(90deg, var(--primary) 0%, #2D5A3F 100%);
    color: white;
}
```

---

## 🚀 Instalación
No requiere compilación. Simplemente clona el repositorio y abre `index.html` en tu navegador favorito.

```bash
git clone https://github.com/aemsyncgd/cocina-economica.git
```

---
*Desarrollado con pasión para una cocina más inteligente y eficiente.*
