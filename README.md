# Zymar Streaming – Web / PWA

Página responsive y profesional que carga tu Google Apps Script dentro de una app instalable (PWA), lista para Vercel y **sin caché**.

## Archivos
- `index.html` – interfaz (header, splash de carga, pantalla completa, manejo de errores/offline, banner de instalación)
- `vercel.json` – cabeceras `no-store` para evitar caché en Vercel (CDN y navegador)
- `sw.js` – service worker que NO guarda caché (solo permite instalar la app)
- `manifest.webmanifest` + `icon.svg` – configuración de app móvil

## Desplegar en Vercel
1. Sube esta carpeta a un repositorio de GitHub (o usa `vercel` desde la terminal dentro de la carpeta).
2. En Vercel: **Add New → Project** → selecciona el repo → **Deploy** (Framework: *Other*, sin build).

## IMPORTANTE: permitir que Apps Script se muestre dentro de la página
En tu código de Apps Script (`doGet`), si usas `HtmlService`, debes permitir el embebido:

```javascript
function doGet() {
  return HtmlService.createHtmlOutputFromFile('index')
    .setTitle('Zymar')
    .setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL);
}
```

Y en **Implementar → Administrar implementaciones**: ejecutar como *Yo* y acceso *Cualquier persona*. Después de cambiar el código, crea una **nueva versión** de la implementación.

Si no haces esto, el navegador bloqueará el iframe y la página mostrará el botón **"Abrir directo"**.

## Cambiar la URL
En `index.html`, variable `APP_URL`.
