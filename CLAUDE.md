# CLAUDE.md — BRANCA Fitness Club

> Documento vivo. Leer al inicio de cada sesión. Actualizar con cada corrección del usuario.

---

## 🎯 Qué es esto

Sitio web one-page del gimnasio **BRANCA Fitness Club** (Montevideo, Uruguay).
Dueño: Lucas (no técnico — el asistente maneja todo lo técnico con tokens).

- **Dominio:** brancafitnes.com (una sola "s" en fitness)
- **Hosting:** Netlify
- **Site ID Netlify:** `3da4a017-3479-45fc-a480-a59221989ca3`
- **GitHub repo:** https://github.com/suarez01lucas-commits/branca-fitnes.git

---

## 🧱 Stack

- HTML + CSS + JS vanilla, **sin build step**, todo en `index.html`
- Fuentes: Google Fonts (Bebas Neue + Montserrat)
- Imágenes: archivos `.JPG`/`.PNG` locales en la raíz
- `_headers` → security headers para Netlify (CSP, X-Frame, etc.)

**No hay:** package.json, framework, bundler, tests automatizados.

---

## 📐 Estructura de `index.html`

Una sola página con 7 secciones (ancla `id=`):

| Sección | id | Líneas aprox |
|---|---|---|
| Hero / Inicio | `inicio` | 986 |
| Planes | `planes` | 1018 |
| Modalidades | `modalidades` | 1100 |
| Sobre Branca | `sobre` | 1168 |
| Ubicación | `ubicacion` | 1203 |
| Horarios | `horarios` | 1245 |
| Contacto | `contacto` | 1346 |

Estilos en `<style>` inline al inicio. Variables CSS en `:root` (colores, radios, max-width).

---

## 🎨 Diseño

- **Colores:** negro `#0a0a0a` + dorado `#C9A227` (variables `--black`, `--gold`)
- **Tipografías:** Bebas Neue (títulos), Montserrat (texto)
- Border radius: `16px` (`--radius`)
- Max width: `1200px` (`--max-width`)
- **Logo:** `logo-branca.png` (metálico dorado, fondo transparente, 500x284). Reemplazó al logo de texto.

## 📦 Planes (actualizado 2026-05-21)

4 planes con prefijo "Branca":
1. **Branca Básico** — img `40cb8827-...JPG`
2. **Branca Program** — img `7d905b70-...JPG`
3. **Branca Personal** — img `9e166f80-...JPG` (con badge "Popular")
4. **Branca Nutrition** — img `35b09f6f-...JPG`

En desktop grid es 4 columnas (>=1024px), 2 columnas en tablet (640-1024), 1 en mobile.

---

## 📞 Datos del gym

- **Dirección:** Cerro Largo 1157 esq. Av. Libertador, Montevideo
- **WhatsApp:** 097 194 546 → link `wa.me/59897194546`
- **Instagram:** @brancafitnessclub

---

## 🚀 Deploy

```bash
# 1. Editar /Users/admin/Branca fitness/index.html

# 2. Crear ZIP excluyendo archivos pesados/innecesarios
cd "/Users/admin/Branca fitness"
zip -r /tmp/branca-deploy.zip . -x "*.git*" -x ".DS_Store" -x "CLAUDE.md"

# 3. Deploy a Netlify (token en memoria, archivo credentials.md)
curl -X POST "https://api.netlify.com/api/v1/sites/3da4a017-3479-45fc-a480-a59221989ca3/deploys" \
  -H "Authorization: Bearer <NETLIFY_TOKEN>" \
  -H "Content-Type: application/zip" \
  --data-binary @/tmp/branca-deploy.zip
```

Después del deploy, **commitear a git también** para que el repo refleje lo que está online.

---

## 🧪 Verification loop (regla 5)

Antes de decir "listo":
1. ¿Abrir `index.html` en navegador local? (al menos visual check)
2. ¿Después del deploy, abrir brancafitnes.com y verificar la sección cambiada?
3. ¿Cambios commiteados en git?

**Nunca declarar "listo" sin verificar visualmente que se ve bien en la web pública.**

---

## ❌ NO HACER

> Cada vez que el user corrige algo, agregar la regla acá.

- ❌ **No deployar sin commitear después.** Repo y producción no pueden divergir.
- ❌ **No incluir las fotos PNG sueltas (`IMG_9069.PNG` etc.) en el ZIP del deploy** salvo que se usen en el HTML. Pesan mucho y no aportan.
- ❌ **No tocar el `_headers`** sin avisar — la CSP está afinada y romperla puede tirar fuentes/imágenes.
- ❌ **No pedirle al usuario que haga cosas técnicas** (subir archivos, copiar tokens, etc.). Lucas no es técnico. Usar tokens y resolver yo.
- ❌ **No cambiar el dominio "brancafitnes" a "brancafitness"** — está registrado con una sola "s" a propósito.
- ❌ **No confiar en Chrome headless para verificar mobile.** Headless Chrome IGNORA el viewport meta tag y renderiza a ~500-980px aunque pongas `--window-size=375,xxx`. Cualquier "clipping" visible en headless puede ser solo artefacto. Para verificación mobile real, abrir en Safari/Chrome con DevTools mobile mode o pedirle al usuario que confirme desde el celu.
- ❌ **No usar `display: flex` en una section sin asegurar que `.container` hijo tenga `flex: 1 1 100%` o `width: 100%`.** Si no, el container toma su ancho intrínseco (el del contenido más ancho) y rompe el responsive. El hero (`#inicio`) ya tiene la fix aplicada.

---

## 🛠️ Comandos comunes

```bash
# Ver estructura
ls "/Users/admin/Branca fitness/"

# Ver secciones del HTML
grep -n '<section ' index.html

# Diff con el último commit
git diff index.html

# Historia
git log --oneline -30

# Build ZIP de deploy
cd "/Users/admin/Branca fitness" && zip -r /tmp/branca-deploy.zip . -x "*.git*" -x ".DS_Store" -x "CLAUDE.md"
```

---

## 🧭 Reglas operativas globales

Aplicar siempre las 8 reglas de Compounding Engineering (cargadas en memoria del asistente):

1. 🔍 Explorar antes de codear
2. 📜 Preguntar al historial de git
3. 📄 CLAUDE.md vivo (este archivo)
4. 📋 Plan mode antes de features grandes
5. 🔄 Verification loops obligatorios
6. 🧠 Editar CLAUDE.md después de cada corrección
7. ⚙️ MCPs y skills FIRST
8. 🚀 Paralelismo con git worktrees

**Principio:** cada corrección documentada hoy hace que el sistema sea mejor para siempre.
