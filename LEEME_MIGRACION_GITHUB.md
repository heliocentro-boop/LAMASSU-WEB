# Migración a GitHub Pages — LAMASSU Security Consulting

## ✅ Rebranding completado — HEIMDALL → LAMASSU

Toda la web (home + 10 subpáginas + páginas legales) ya dice **LAMASSU
Security Consulting**, con el dominio **lamassu-security.es** en todos los
enlaces, emails y metadatos. El logo hexagonal ahora muestra las iniciales
**"LMSS"** (hexágono anidado, mismo diseño que ya conocías, solo con las
letras nuevas), tanto en la home como en las 10 subpáginas.

## ✅ Los 6 PNG de marca también actualizados

Los 6 archivos de `assets/img/` (banners, icono, logos de perfil) se
reconstruyeron desde cero manteniendo exactamente el mismo diseño, colores
y geometría del hexágono que los originales — solo se sustituyó el texto
"HM"/"HEIMDALL" por "LMSS"/"LAMASSU". De paso, los dos banners (LinkedIn
y Twitter/X) quedaron sin el fallo de texto superpuesto/doble exposición
que tenían antes, porque al reconstruirlos con código no se arrastra ese
defecto.



## PASO 1 — Crear el repositorio en GitHub

1. Entra en https://github.com y crea una cuenta si no tienes una
2. Botón "New repository"
3. Nombre sugerido: `lamassu-web` (o el que prefieras — no tiene que
   coincidir con el dominio)
4. **Marca el repositorio como Público** — GitHub Pages gratis solo
   funciona con repos públicos (los privados requieren plan de pago
   GitHub Pro/Team). Esto significa que cualquiera podrá ver el código
   fuente de la web (no hay contraseñas ni datos sensibles en él, ya
   quité los documentos internos de esta carpeta).
5. Crea el repositorio vacío (sin README, sin .gitignore)

## PASO 2 — Subir los archivos

Opción sencilla sin usar la terminal:
1. En la página del repositorio recién creado, pulsa "uploading an
   existing file"
2. Arrastra **todo el contenido** de esta carpeta (`para-github-pages/`),
   manteniendo la estructura de subcarpetas (`assets/`, `documentos/`)
3. Commit directamente a la rama `main`

Opción con git (si te manejas con la terminal):
```
cd para-github-pages
git init
git add .
git commit -m "Primera versión de la web"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/lamassu-web.git
git push -u origin main
```

## PASO 3 — Activar GitHub Pages

1. En el repositorio, ve a **Settings → Pages**
2. En "Source", elige la rama `main` y la carpeta `/ (root)`
3. Guarda. GitHub te dará una URL provisional tipo
   `https://tu-usuario.github.io/lamassu-web/` — pruébala primero ahí
   antes de conectar el dominio propio

## PASO 4 — Conectar el dominio lamassu-security.es

**Primero en GitHub** (antes de tocar el DNS, para evitar que alguien
más pueda apropiarse del dominio mientras tanto):
1. Settings → Pages → "Custom domain" → escribe `lamassu-security.es`
   → Save
   (esto ya está pre-configurado en el archivo `CNAME` que subiste, pero
   conviene confirmarlo aquí también)

**Luego en tu proveedor de dominio** (donde compres `lamassu-security.es`
— Arsys, Hostinger, nic.es...), añade estos registros DNS:

| Tipo | Nombre/Host | Valor |
|---|---|---|
| A | @ (o vacío) | 185.199.108.153 |
| A | @ (o vacío) | 185.199.109.153 |
| A | @ (o vacío) | 185.199.110.153 |
| A | @ (o vacío) | 185.199.111.153 |
| CNAME | www | tu-usuario.github.io |

(Estas son las IPs oficiales de GitHub Pages, verificadas en su
documentación — no cambian según el proyecto.)

La propagación puede tardar desde unos minutos hasta 24-48h. Cuando
GitHub detecte el DNS correcto, activa automáticamente el certificado
SSL gratuito (candado https) — puede tardar un rato extra en aparecer
la opción "Enforce HTTPS" en Settings → Pages.

## PASO 5 — Activar el formulario de contacto (Formspree)

El formulario **no funcionará hasta que hagas esto** — actualmente
apunta a un ID de ejemplo (`XXXXXXXX`):

1. Crea cuenta gratuita en https://formspree.io
2. Nuevo formulario → email de destino: la cuenta de correo donde quieras
   recibir las consultas (recuerda que `info@lamassu-security.es` aún
   no existe hasta que compréis el dominio y deis de alta el correo)
3. Copia el ID que te dan (ej: `xpzgvkra`)
4. Abre `index.html`, busca `FORMSPREE_ENDPOINT` (aparece una vez, cerca
   de la línea 1200) y sustituye `XXXXXXXX` por tu ID real
5. Vuelve a subir el archivo al repositorio

**Limitación del plan gratuito de Formspree:** 50 envíos al mes, y no
admite archivos adjuntos (por eso quité el campo de "adjuntar
documentación" del formulario en esta versión — ahora pide al usuario que
escriba un email aparte si necesita mandar archivos). Si en algún momento
superáis los 50 envíos/mes, hay que pasar a un plan de pago (~15€/mes) o
cambiar de servicio.

## Qué se quitó respecto a la versión de Hostinger

- `process-form.php` — no se ejecuta en GitHub Pages (no soporta PHP)
- El campo de adjuntar archivos en el formulario de contacto
- La carpeta `interno/` (documentos internos: facturas, tarifas, plantillas
  de email) — **nunca debe subirse a un repositorio público**
- La carpeta `referencia/` — igual, uso interno

## Cuando volváis a Hostinger

La carpeta hermana `para-hostinger-mas-adelante/` es una copia exacta
de la web tal y como estaba funcionando con PHP, sin ningún cambio — está
lista para subir tal cual el día que decidáis volver a Hostinger. No hace
falta deshacer nada del cambio a GitHub: son dos carpetas independientes.
