# Red Flag Report

Dashboard interactivo que consume registros de un Google Sheet público para exponer “expedientes” de red flags. Usa Tailwind vía CDN + Chart.js y tiene un fuerte enfoque mobile:

- **Modo Swipe Prioritario**: experiencia tipo Tinder que ordena los casos por dramatismo, permite filtrar por departamento y muestra chips, alertas y progress bars antes de abrir el modal completo.
- **Panel analítico**: KPIs, radar de patrones, barras de profesiones/departamentos y tablas responsivas con paginación y búsqueda.
- **Datos**: se cargan en caliente desde `gviz/tq` (Sheets) con fallback a `datos/html/info.html`.

### Stack
* HTML5 + Tailwind (CDN)
* Chart.js para gráficas
* JavaScript vanilla (DOMParser, FileReader, fetch, etc.)

### Flujo de uso
1. Abrir `index.html` sirviéndolo mediante `python -m http.server` o similar (para evitar restricciones de `fetch`).
2. El dashboard intenta cargar automáticamente el Sheet remoto; si falla, usa el HTML local.
3. Modo Swipe → KPIs → Hall of Shame → Lista Negra (con tabla optimizada para mobile).

### Personalización rápida
- **Fuente de datos**: modificar `REMOTE_DATA_URL` o actualizar `datos/html/info.html`.
- **Busqueda/filters**: `filterTable`, `populateDeptFilter`.
- **Métricas**: `analyzeAndRender` calcula KPIs; agregar palabras clave al objeto `patterns`.
