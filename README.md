# Sergio Rosa y Asociados

Sitio del estudio jurídico de San Pedro, Buenos Aires.

**Doce páginas: la home y una por área de práctica.** Las tipografías, las fotos, la hoja de
estilos y el JavaScript son archivos aparte dentro de `assets/`, compartidos por las doce: el
navegador los baja una vez y los reusa. Sin framework y sin dependencias externas.

## Las dos versiones

Del mismo fuente salen dos cosas, y cada una sirve para algo distinto:

| | Para qué | Peso |
|---|---|---|
| `index.html` + `assets/` + las once carpetas | **La web.** Es lo que se publica. | 57 KB la home, 40 KB cada área |
| `sergio-rosa-para-mostrar.html` | **Para mandar.** Un archivo con todo adentro: abre con doble clic, sin servidor, sin internet y sin la carpeta al lado. | ~1 MB |

La portable se genera, no se edita. Si hay que cambiar algo se cambia en la web y se vuelve a
generar (ver *Cómo se arma*).

## Qué hay acá

| | |
|---|---|
| `index.html` | la home |
| `accidentes-de-transito/`, `derecho-laboral/`, … | una carpeta por área, once en total |
| `assets/estilos.css` | la hoja de estilos, con los `@font-face` adentro |
| `assets/sitio.js`, `assets/sitio-2.js` | el JavaScript |
| `assets/fonts/` | Inter e Inter Tight, subset latino, variables 400-900 |
| `assets/img/` | las fotos publicadas, en webp |
| `assets/*.jpg` | los originales de las fotos, para poder rehacerlas |
| `sergio-rosa-para-mostrar.html` | la copia portable (generada) |

## Cómo se arma

Los generadores viven en `design/`, que no se publica. El orden importa: cada paso da por hecho
lo que hizo el anterior, y todos cortan con un mensaje claro si algo no está donde esperaban.

```bash
node design/extraer-assets.mjs       # saca de index.html las fuentes y fotos embebidas
node design/externalizar.mjs         # y las reemplaza por rutas
node design/externalizar-css-js.mjs  # saca la hoja de estilos y los dos scripts
node design/enlazar-areas.mjs        # apunta las tarjetas y el pie a las once páginas
node design/build-areas.mjs          # genera las once páginas de área
node design/hacer-portable.mjs       # arma la copia de un solo archivo
```

Verificadores, en `design/`:

```bash
node design/_check.mjs         # estructura, h1, enlaces internos de las doce
node design/_check-assets.mjs  # que todo cargue, por file:// y por HTTP
node design/_medir.mjs         # cuántos KB baja realmente un visitante
```

## Cómo está hecho

Once áreas de práctica, ficha por abogado, formulario en cuatro pestañas y mapa. HTML, CSS y
JavaScript a mano, con [GSAP](https://gsap.com) para las animaciones atadas al scroll.

Tres cosas que se sostienen a propósito:

- **Funciona sin JavaScript.** El contenido está en el HTML; las animaciones son un agregado
  encima. Si el script no corre, la página se lee igual.
- **Respeta `prefers-reduced-motion`.** A quien tiene configurado que no quiere movimiento, la
  página le llega quieta y completa.
- **Cero CDN.** Las tipografías son archivos nuestros. Nada del sitio depende de un tercero.

## Indexación

✅ **Las doce páginas están abiertas a Google desde el 31-08.** Hasta ese día las once de área
llevaban `<meta name="robots" content="noindex, nofollow">` y la home no, así que lo único
indexable era la página sin datos estructurados. El `meta` salía de `design/build-areas.mjs`, no
de los archivos: sacarlo a mano de los once HTML no alcanzaba, porque el generador los pisa cada
vez que se toca la home.

- `sitemap.xml` — las doce URL. 🔴 **Hay que cargarlo a mano en Google Search Console**, no se
  descubre solo (ver la razón en `robots.txt`).
- `robots.txt` — escrito, pero **hoy no lo lee nadie**: en un project page de GitHub los
  rastreadores leen `seerystudio.github.io/robots.txt`, no el nuestro. Empieza a regir
  el día del dominio propio.

## Antes de publicar

- Falta el dominio propio. Cuando esté: las doce URL del `sitemap.xml`, las claves `url` de los
  datos estructurados (`LegalService`, `BreadcrumbList`, `FAQPage`), y `canonical` y Open Graph,
  que hoy **no existen en ninguna de las doce**.
- La home no tiene datos estructurados. Los `LegalService` / `BreadcrumbList` / `FAQPage` viven
  sólo en las páginas de área.
- El bloque de reseñas de la home está tapado con `display:none`: la ficha de Google existe pero
  tiene cero reseñas. O se cargan reales, o el bloque se borra.
