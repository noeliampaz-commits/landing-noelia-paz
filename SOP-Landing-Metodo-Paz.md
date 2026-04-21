# SOP — Landing Page Método Paz (noeliapaz.com)

Manual operativo completo para mantener, actualizar y deployar la landing page del Método Paz.

---

## 1. RESUMEN GENERAL

| Item | Detalle |
|---|---|
| URL producción | https://www.noeliapaz.com |
| URL fallback | https://landing-noelia-paz.vercel.app |
| Repositorio | https://github.com/noeliampaz-commits/landing-noelia-paz |
| Branch | `main` |
| Hosting | Vercel (cuenta Hobby, proyecto `landing-noelia-paz`) |
| Dominio | GoDaddy → DNS apuntando a Vercel |
| Analytics | Google Analytics 4 — ID: `G-XXR2QHELMF` |
| CTA final | Calendly embebido: `https://calendly.com/d/cxsv-7kb-xbg` |
| Auto-deploy | Push a `main` → Vercel redeploya en ~1 min |

---

## 2. ESTRUCTURA DE ARCHIVOS

```
landing/
├── index.html                ← TODO el sitio (HTML + CSS + JS en un archivo)
├── .gitignore                ← excluye MP4 raíz, .env, etc.
├── vercel.json               ← redirects para shortlinks UTM
├── logo.jpg                  ← logo Método Paz (header + favicon)
├── noe-paz.webp              ← foto de Noe para sección "Sobre la experta"
├── img/                      ← fotos testimoniales (antes/después)
│   ├── ale1.png
│   ├── ale2.png
│   ├── ana.jpeg
│   ├── andrea.jpg
│   ├── astrid.jpg
│   ├── betiana.jpeg
│   ├── cari.png
│   ├── constanza.png
│   ├── cris.jpeg
│   ├── dani.jpeg
│   ├── elen.png
│   ├── euge.png
│   ├── flor.jpeg
│   ├── gaby.png
│   ├── graciela.png
│   ├── magui.png
│   ├── marce.png
│   ├── patricia1.jpg
│   ├── patricia2.jpeg
│   ├── sil.png
│   ├── sole.jpeg
│   └── vanesa.jpg
├── testimonios/              ← videos testimoniales (comprimidos para web)
│   ├── Alejandrian testimonio.mp4   (13MB, Ale)
│   ├── Testimonio Marcela.mp4       (6MB)
│   ├── Testimonio Yazmin.mp4        (11MB)
│   └── original/                    ← originales sin comprimir (NO se deployean)
├── vsl.mp4                   ← VSL local (NO se deploya, va por YouTube)
├── Método Paz lq.mp4         ← versión baja calidad (NO se deploya)
├── DEPLOY-RESUMEN.md
├── PASOS-PENDIENTES.md
└── SOP (este archivo)
```

**Nota:** `.gitignore` excluye `*.mp4` pero permite `!testimonios/*.mp4`. Los MP4 en la raíz (vsl.mp4, etc.) NO se suben al repo. El VSL se embebe desde YouTube.

---

## 3. SECCIONES DE LA LANDING (orden actual)

| # | Sección | Línea aprox. | ID/Anchor |
|---|---|---|---|
| 1 | Header (logo) | 1091 | — |
| 2 | Hero (H1 + VSL + proof-bar + CTA) | 1098 | — |
| 3 | Resultados (videos + fotos agrupadas) | 1134 | `#resultados` |
| 4 | Pain Points (¿Te sentís identificada?) | 1445 | `#dolor` |
| 5 | Future Pacing (Tu vida después) | 1513 | — |
| 6 | 3 Pilares del Método Paz | 1557 | `#metodo` |
| 7 | ¿Cómo funciona? (4 cards) | 1587 | `#programa` |
| 8 | ¿Es para vos? (Sí/No) | 1620 | — |
| 9 | Sobre Noe Paz | 1651 | `#sobre-noe` |
| 10 | FAQ (acordeón) | 1690 | `#faq` |
| 11 | CTA Final + Calendly | 1755 | `#agendar` |
| 12 | Footer | 1835 | — |

---

## 4. DISEÑO Y SISTEMA VISUAL

### Colores
| Variable | Valor | Uso |
|---|---|---|
| `--bg-deep` | `#050505` | Fondo principal |
| `--bg-card` | `#121212` | Cards, containers |
| `--accent` | `#C18F12` | Dorado principal (botones, highlights) |
| `--accent-light` | `#D4A82A` | Dorado claro |
| `--text-primary` | `#F5F5F0` | Texto principal (crema) |
| `--text-muted` | `#8A8A80` | Texto secundario |

### Tipografía
- **Headings:** Cormorant Garamond (serif, Google Fonts)
- **Body:** Jost (sans-serif, Google Fonts)

### Botón CTA (todos iguales)
Formato 2 líneas:
- Línea 1 (grande): **TRANSFORMA TU ALIMENTACIÓN Y SALUD**
- Línea 2 (chica): **ACCEDE AHORA**
- Background: gradient dorado
- Color texto: negro (#050505)
- Todos linkan a `#agendar` (Calendly al final)

### Animaciones
- **Scroll Reveal:** elementos aparecen al hacer scroll (IntersectionObserver)
- **Counter animado:** proof-bar cuenta de 0 al target (15, 8 kg, 90)
- **Progress bar:** barra dorada arriba que muestra % de scroll

---

## 5. CÓMO AGREGAR UN NUEVO TESTIMONIO CON FOTO

### Paso 1: Preparar la imagen
- Formato: `.jpg`, `.jpeg`, o `.png`
- Tamaño recomendado: 400-600px de ancho (no necesita ser gigante)
- Nombre: usar nombre en minúsculas sin espacios (ej: `maria.jpg`)
- Copiar la imagen a la carpeta `landing/img/`

### Paso 2: Agregar el HTML
Abrir `index.html` y buscar el grupo correcto según los días del resultado:

- **90 días:** buscar `<!-- Fotos: 90 días -->`
- **60 días:** buscar `<!-- Fotos: 60 días -->`
- **30 días:** buscar `<!-- Fotos: 30 días -->`

Dentro del `<div class="testimonials-grid">` correspondiente (o `testimonials-grid--centered` para 60/30 días), agregar este bloque:

```html
      <div class="testimonial-card reveal">
        <span class="quote-mark">&ldquo;</span>
        <div class="testimonial-img-wrap"><img src="img/NOMBRE.jpg" alt="NOMBRE - antes y después" class="testimonial-img" loading="lazy"></div>
        <div class="testimonial-highlight">
          <span class="testimonial-kg">-X</span>
          <span class="testimonial-kg-label">kilos</span>
        </div>
        <div class="testimonial-name">NOMBRE</div>
        <p class="testimonial-result">DESCRIPCIÓN DEL RESULTADO.</p>
      </div>
```

**Reemplazar:**
- `NOMBRE.jpg` → nombre del archivo de imagen
- `NOMBRE` → nombre de la clienta
- `-X` → kilos perdidos (con signo negativo)
- `DESCRIPCIÓN DEL RESULTADO` → texto corto del resultado

**Si tiene condición médica especial**, agregar después del `<p>` de resultado:
```html
        <span class="testimonial-badge">Con endometriosis</span>
```

### Paso 3: Respetar el orden
- Dentro de cada grupo de días, las cards van **ordenadas por kilos perdidos de mayor a menor** (-10, -9, -8, -7, etc.)
- Insertar la nueva card en la posición correcta según sus kilos

### Paso 4: Clase reveal
- Alternar entre `reveal`, `reveal reveal-delay-1`, y `reveal reveal-delay-2` para el efecto de aparición escalonada (ciclo de 3)

---

## 6. CÓMO AGREGAR UN NUEVO TESTIMONIO EN VIDEO

### Paso 1: Comprimir el video
Los videos deben estar comprimidos para web. Usar ffmpeg:

```bash
ffmpeg -y -i "VIDEO_ORIGINAL.mp4" \
  -vf "scale='min(720,iw)':'-2'" \
  -c:v libx264 -preset medium -crf 26 \
  -movflags +faststart \
  -c:a aac -b:a 96k -ac 1 \
  "VIDEO_COMPRIMIDO.mp4"
```

Esto genera un video de ~5-15MB en 720p, óptimo para web.

### Paso 2: Guardar el video
- Copiar el video comprimido a `landing/testimonios/`
- Guardar el original en `landing/testimonios/original/`

### Paso 3: Agregar el HTML
Buscar `<!-- Videos testimoniales -->` en `index.html`. Dentro del `<div class="video-testimonials-grid">`, agregar:

```html
      <div class="video-testimonial-card reveal">
        <div class="vt-name">NOMBRE:</div>
        <video controls preload="metadata" playsinline>
          <source src="testimonios/ARCHIVO.mp4" type="video/mp4">
        </video>
        <div class="vt-footer">
          <div class="vt-time">En solo 90 días</div>
          <div class="vt-result">DESCRIPCIÓN DEL RESULTADO</div>
        </div>
      </div>
```

**Reemplazar:**
- `NOMBRE` → nombre de la clienta
- `ARCHIVO.mp4` → nombre del archivo (si tiene espacios, reemplazarlos por `%20` en el `src`)
- `90 días` → duración real
- `DESCRIPCIÓN DEL RESULTADO` → texto en mayúsculas del resultado

### Paso 4: Actualizar .gitignore
Si es la primera vez que se agrega un video, verificar que `.gitignore` tenga:
```
*.mp4
!testimonios/*.mp4
```

---

## 7. CÓMO DEPLOYAR CAMBIOS

### Requisitos
- Git instalado
- Acceso al repo (PAT de GitHub de la cuenta `noeliampaz-commits`)

### Pasos

```bash
# 1. Ir a la carpeta de la landing
cd "/Users/julian/Desktop/AI Players/Clientes/Noelia Paz/landing"

# 2. Ver qué cambió
git status
git diff

# 3. Agregar los archivos modificados (NUNCA usar git add . a ciegas)
git add index.html                    # si cambió el HTML
git add img/nueva-foto.jpg            # si agregaste fotos
git add testimonios/nuevo-video.mp4   # si agregaste videos

# 4. Commit con descripción clara
git commit -m "agregar testimonio de María (-6 kg, 90 días)"

# 5. Push (Vercel redeploya automático)
git push https://TOKEN@github.com/noeliampaz-commits/landing-noelia-paz.git main
```

**Si el push falla con "Permission denied":** el token expiró. Generar nuevo PAT en GitHub Settings → Developer settings → Personal access tokens.

### Verificación post-deploy
1. Esperar ~1 min
2. Abrir https://www.noeliapaz.com con hard refresh (Cmd+Shift+R)
3. Verificar:
   - [ ] Desktop: todas las secciones cargan
   - [ ] Mobile: scroll, videos, botones
   - [ ] Videos testimoniales reproducen
   - [ ] VSL reproduce con autoplay
   - [ ] Calendly carga y se puede agendar
   - [ ] Botones llevan a `#agendar`
   - [ ] GA4 Realtime muestra la visita

---

## 8. UTM TRACKING (Shortlinks)

Configurados en `vercel.json` como redirects 307.

| Shortlink | Uso | URL completa |
|---|---|---|
| noeliapaz.com/ig | Bio de Instagram | `?utm_source=instagram&utm_medium=bio&utm_campaign=evergreen` |
| noeliapaz.com/stories | Stories | `?utm_source=instagram&utm_medium=stories&utm_campaign=evergreen` |
| noeliapaz.com/dm | DM de Instagram | `?utm_source=instagram&utm_medium=dm&utm_campaign=evergreen` |
| noeliapaz.com/post | Post de Instagram | `?utm_source=instagram&utm_medium=post&utm_campaign=evergreen` |
| noeliapaz.com/reel | Reel de Instagram | `?utm_source=instagram&utm_medium=reel&utm_campaign=evergreen` |
| noeliapaz.com/wa | WhatsApp directo | `?utm_source=whatsapp&utm_medium=direct&utm_campaign=evergreen` |
| noeliapaz.com/email | Newsletter | `?utm_source=email&utm_medium=newsletter&utm_campaign=evergreen` |
| noeliapaz.com/yt | YouTube descripción | `?utm_source=youtube&utm_medium=description&utm_campaign=evergreen` |
| noeliapaz.com/tt | TikTok bio | `?utm_source=tiktok&utm_medium=bio&utm_campaign=evergreen` |
| noeliapaz.com/ttvideo | TikTok video | `?utm_source=tiktok&utm_medium=video&utm_campaign=evergreen` |

### Agregar un shortlink nuevo
Editar `vercel.json` y agregar un nuevo objeto en el array `redirects`:
```json
{
  "source": "/SHORTLINK",
  "destination": "/?utm_source=FUENTE&utm_medium=MEDIO&utm_campaign=CAMPAÑA",
  "permanent": false
}
```

Los UTMs se pasan automáticamente al widget de Calendly (hay un script en el HTML que lo hace).

### Para campañas específicas
Usar URL larga cambiando el `utm_campaign`:
```
https://www.noeliapaz.com/?utm_source=instagram&utm_medium=stories&utm_campaign=lm_hormonas
```

---

## 9. CALENDLY

### Configuración actual
- **URL del evento:** `https://calendly.com/d/cxsv-7kb-xbg`
- **Colores del embed:** fondo `#121212`, texto `#f5f5f0`, primary `#c18f12`
- **GDPR banner:** oculto (`hide_gdpr_banner=1`)
- **Tracking:** los UTMs de la landing se pasan al widget automáticamente
- **GA4:** cuando alguien confirma un booking, se dispara evento `generate_lead` en GA4

### Cambiar el evento de Calendly
Si cambia la URL del evento, buscar en `index.html` todas las ocurrencias de `calendly.com/d/cxsv-7kb-xbg` y reemplazarlas (hay ~3: widget, noscript fallback, y posiblemente en scripts).

### Cambiar colores del Calendly
Los colores se configuran en 2 lugares:
1. **URL del widget** (parámetros `background_color`, `text_color`, `primary_color` en el `data-url`)
2. **Panel de Calendly** (Evento → Inserción en línea → Personalizar). Los del panel tienen prioridad.

---

## 10. ANALYTICS (GA4)

### Datos de la cuenta
| Item | Valor |
|---|---|
| Propiedad | Método PAZ |
| ID de medición | `G-XXR2QHELMF` |
| ID de flujo | 14369131322 |
| Medición mejorada | ON (scrolls, outbound clicks, video, downloads) |

### Eventos personalizados
- `generate_lead` — se dispara cuando alguien confirma booking en Calendly

### Acceder a los datos
1. Ir a https://analytics.google.com
2. Seleccionar propiedad "Método PAZ"
3. Reportes → Realtime para verificar que trackea
4. Reportes → Adquisición → Tráfico para ver por fuente/medio (UTMs)

---

## 11. VSL (Video de Ventas)

### Configuración actual
- **Fuente:** YouTube embed (video ID: `tiscowFP_jk`)
- **Comportamiento:** autoplay, muted, loop, playsinline
- **Diseño:** contenedor con border-radius 14px, border dorado sutil, shadow

### Cambiar el video
1. Subir el nuevo video a YouTube
2. Copiar el ID del video (la parte después de `v=` en la URL)
3. En `index.html`, buscar `tiscowFP_jk` y reemplazar por el nuevo ID (aparece 2 veces: en el iframe `src` y en el `playlist` param para el loop)

---

## 12. DATOS IMPORTANTES DEL NEGOCIO (para copy)

Estos datos son fijos y no deben cambiarse sin aprobación de Noe:

| Dato | Valor | Nota |
|---|---|---|
| Años de experiencia | **15** | NO 30 (Noe lo corrigió explícitamente) |
| Resultado prometido | Hasta **8 kg** en **90 días** | Con ganancia muscular |
| Target | Mujeres profesionales **35-55**, perimenopausia | — |
| Diferencial | Alimentación antiinflamatoria a base de **plantas y sin gluten** | NO es dieta |
| Noe es | **Chef** especialista | Fundadora Casa II Restaurante, BsAs |

### 3 Pilares del Método (orden oficial)
1. Protocolo de ayuno — detox intestinal
2. Alimentación antiinflamatoria — coaching + recetario
3. Equilibrio de eje hormonal

---

## 13. TROUBLESHOOTING

### "El push a GitHub falla con Permission denied"
El PAT (Personal Access Token) expiró. Generar uno nuevo en GitHub → Settings → Developer settings → Personal access tokens. Usar:
```bash
git push https://NUEVO_TOKEN@github.com/noeliampaz-commits/landing-noelia-paz.git main
```

### "Los cambios no se ven en la landing"
1. Verificar que el push fue exitoso (`git log` muestra el commit)
2. Esperar ~1-2 min (Vercel redeploya)
3. Hard refresh: Cmd+Shift+R (Mac) o Ctrl+Shift+R (Windows)
4. Probar en ventana de incógnito

### "Un video no reproduce"
- Verificar que el archivo está en `testimonios/` y que el nombre en el HTML coincide exactamente (incluyendo mayúsculas y espacios → usar `%20`)
- Verificar que `.gitignore` tiene `!testimonios/*.mp4`
- Verificar que el video fue pusheado (`git status` no debería mostrarlo como untracked)

### "El Calendly no carga"
- Verificar conexión a internet
- El script de Calendly se carga async — puede tardar unos segundos
- Si no carga, aparece un link directo como fallback (`<noscript>`)

### "Quiero cambiar el dominio"
- El dominio está en GoDaddy. DNS actual: `A @ → 216.198.79.1` (Vercel), `CNAME www → cname.vercel-dns.com`
- Si se cambia de dominio, actualizar en Vercel → Project Settings → Domains

---

## 14. CONTACTOS Y ACCESOS

| Servicio | Cuenta | Notas |
|---|---|---|
| GitHub | `noeliampaz-commits` | Repo público |
| Vercel | `noeliampaz-3723` (Hobby) | Auto-deploy desde GitHub |
| GoDaddy | (cuenta de Noe) | Dominio noeliapaz.com |
| GA4 | Propiedad "Método PAZ" | ID: G-XXR2QHELMF |
| Calendly | (cuenta de Noe) | Evento: Método Paz Admisión |
| YouTube | Canal de Noe | VSL: tiscowFP_jk |

---

*Última actualización: abril 2026*
