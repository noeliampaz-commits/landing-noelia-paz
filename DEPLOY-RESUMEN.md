# Landing Método Paz — Resumen de Deploy

## Producción
- **URL principal:** https://www.noeliapaz.com
- **Redirect apex:** https://noeliapaz.com → www (307)
- **SSL:** activo (automático Vercel)

## Infraestructura

### GitHub
- **Cuenta:** `noeliampaz-commits`
- **Repo:** https://github.com/noeliampaz-commits/landing-noelia-paz
- **Visibilidad:** public
- **Branch:** main

### Vercel
- **Cuenta:** `noeliampaz-3723` (Hobby)
- **Proyecto:** `landing-noelia-paz`
- **Dominios configurados:**
  - noeliapaz.com (redirect 307 → www)
  - www.noeliapaz.com (production)
  - landing-noelia-paz.vercel.app (fallback)
- **Auto-deploy:** activo (push a main → deploy automático)

### Dominio (GoDaddy)
- **Registrar:** GoDaddy
- **DNS configurados:**
  - A `@` → `216.198.79.1` (apex a Vercel)
  - CNAME `www` → `cname.vercel-dns.com`

## Google Analytics 4
- **Propiedad:** Método PAZ
- **ID de medición:** `G-XXR2QHELMF`
- **ID de flujo:** 14369131322
- **URL flujo:** https://noeliapaz.com
- **Integración:** snippet `gtag.js` en `<head>` de `index.html`
- **Medición mejorada:** ON (scrolls, outbound clicks, site search, video, downloads)

## Shortlinks con UTM tracking
Configurados vía `vercel.json` (redirects 307).

| Shortlink | Canal / Medium | Campaign |
|---|---|---|
| noeliapaz.com/ig | instagram / bio | evergreen |
| noeliapaz.com/stories | instagram / stories | evergreen |
| noeliapaz.com/dm | instagram / dm | evergreen |
| noeliapaz.com/post | instagram / post | evergreen |
| noeliapaz.com/reel | instagram / reel | evergreen |
| noeliapaz.com/wa | whatsapp / direct | evergreen |
| noeliapaz.com/email | email / newsletter | evergreen |
| noeliapaz.com/yt | youtube / description | evergreen |
| noeliapaz.com/tt | tiktok / bio | evergreen |
| noeliapaz.com/ttvideo | tiktok / video | evergreen |

Para campañas específicas, usar el link largo y cambiar `utm_campaign=<nombre>`:
```
https://www.noeliapaz.com/?utm_source=instagram&utm_medium=stories&utm_campaign=lm_hormonas
```

## Archivos del repo
```
landing/
├── .gitignore                ← excluye MP4, node_modules, .env
├── index.html                ← HTML + CSS + JS en un archivo
├── vercel.json               ← redirects de shortlinks
├── logo.jpg
├── noe-paz.webp
├── img/                      ← 22 fotos testimoniales
├── PASOS-PENDIENTES.md       ← checklist original
└── DEPLOY-RESUMEN.md         ← este archivo
```

**Excluidos del repo (no deployar):**
- vsl.mp4
- Método Paz lq.mp4
(El video va embebido desde YouTube: https://youtu.be/22TP7IRsXic)

## Cómo modificar la landing
1. Editar `index.html` localmente.
2. `git add . && git commit -m "descripción" && git push`
3. Vercel detecta el push y redeploya automático en ~1min.
4. Validar en https://www.noeliapaz.com con hard refresh (Cmd+Shift+R).

## Validaciones recomendadas post-deploy
- [ ] Desktop (Chrome, Safari): carga, video, Calendly, CTAs, FAQ, pain points
- [ ] Mobile (iPhone, Android): sticky CTA, scroll animations, video reproduce
- [ ] GA4 Realtime: aparece visita propia
- [ ] Calendly: agendar de prueba y verificar formulario
- [ ] UTMs llegan al Calendly (utm_content = contactid)
- [ ] Shortlinks redirigen correctamente (ej. /ig, /wa)

## Pendientes
- Subir miniatura `vsl-thumbnail.png` al video de YouTube
- Revocar PAT de GitHub usado durante deploy (Settings → Developer settings → PAT → revoke)
- Opcional: generar nuevos PATs o autenticar `gh auth login` a `noeliampaz-commits` para pushes futuros

## Fecha de deploy
2026-04-14
