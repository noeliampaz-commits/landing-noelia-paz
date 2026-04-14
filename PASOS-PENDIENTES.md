# Landing Noelia Paz — Pasos para poner en producción

## 1. Google Analytics 4
- Acceder a Google Analytics (analytics.google.com) con la cuenta de Noe
- Crear propiedad nueva o usar existente
- Configurar flujo de datos web: poner la URL real del sitio de Noe (la de systeme.io o dominio propio)
- Copiar el ID de medición (G-XXXXXXXXXX)
- En index.html, descomentar el bloque de GA4 (líneas 19-27) y reemplazar G-XXXXXXXXXX con el ID real
- Verificar que el evento generate_lead del Calendly se dispare correctamente en GA4

## 2. Acceder a Systeme.io (cuenta de Noe)
- Obtener credenciales de acceso de Noe a systeme.io
- Identificar dónde está hosteada su web actual
- Ver si permite subir HTML/CSS custom o si hay que usar su page builder

## 3. Subir la landing a Systeme.io
- Opción A (HTML custom): subir index.html con todo el CSS inline (ya está todo en un archivo)
- Opción B (page builder): reconstruir en el builder de systeme.io copiando secciones
- Opción C (dominio propio): si tiene dominio, hostear en Vercel/Netlify como hicimos con Lautaro
- Subir todas las imágenes de /img/ y noe-paz.webp
- NO subir vsl.mp4 ni "Método Paz lq.mp4" (el video va embebido desde YouTube)
- Verificar que el video de YouTube embebido funcione (https://youtu.be/22TP7IRsXic)
- Verificar que el Calendly embebido cargue correctamente con los colores (#121212, #f5f5f0, #c18f12)

## 4. Conectar dominio (si aplica)
- Si Noe tiene dominio propio, apuntarlo al hosting
- Configurar SSL/HTTPS

## 5. Testing en producción
- Probar en desktop (Chrome, Safari)
- Probar en mobile (iPhone, Android)
- Verificar que el video se reproduzca
- Verificar que el Calendly funcione y agende correctamente
- Verificar que GA4 trackee visitas (Real-time en Analytics)
- Verificar que UTMs pasen correctamente al Calendly
- Probar todos los CTAs (11 botones apuntan a #agendar)
- Verificar scroll animations, FAQ accordion, pain points interactivos
- Probar sticky CTA en mobile

## 6. Post-deploy
- Subir la miniatura (vsl-thumbnail.png) al video de YouTube
- Crear links con UTMs para cada canal:
  - Instagram: ?utm_source=ig&utm_medium=bio&utm_campaign=metodo_paz
  - WhatsApp: ?utm_source=wa&utm_medium=direct&utm_campaign=metodo_paz
- Compartir link final a Noe para revisión

## Referencia: Landing de Lautaro (ya en producción)
- Seguir el mismo flujo que se usó para deployar la de Lautaro Sorrequieta
- Misma estructura de Calendly embebido con altura dinámica, UTM passthrough, GA4 events

## Archivos de la landing
```
/landing/
├── index.html          ← todo el HTML + CSS + JS en un archivo
├── logo.jpg            ← logo del header
├── noe-paz.webp        ← foto de Noe (sección About)
├── img/                ← 22 fotos de testimonios
│   ├── sole.jpeg, elen.png, astrid.jpg, cari.png...
│   └── (todas las demás)
├── vsl.mp4             ← video comprimido (backup, no subir a producción)
└── Método Paz lq.mp4   ← video original baja calidad (no subir)
```
