# Sergio Rosa y Asociados

Sitio del estudio jurídico de San Pedro, Buenos Aires.

**Es un solo archivo.** [`index.html`](index.html) trae adentro la tipografía, las fotos y el
código, así que abre con doble clic: sin servidor, sin instalar nada y sin internet.

## Cómo verlo

- **En la compu:** doble clic en `index.html`.
- **Para mandárselo a alguien:** el archivo solo alcanza. No hace falta adjuntar `assets/` — las
  fotos ya están adentro del HTML.

## Qué hay acá

| | |
|---|---|
| `index.html` | el sitio |
| `assets/` | las fotos originales del estudio y del equipo, y el logo, para poder rehacerlo |

## Cómo está hecho

Once áreas de práctica, ficha por abogado, formulario en dos pasos y mapa. Sin framework y sin
dependencias: HTML, CSS y JavaScript a mano, con [GSAP](https://gsap.com) para las animaciones
atadas al scroll.

Dos cosas que se sostienen a propósito:

- **Funciona sin JavaScript.** El contenido está en el HTML; las animaciones son un agregado
  encima. Si el script no corre, la página se lee igual.
- **Respeta `prefers-reduced-motion`.** A quien tiene configurado que no quiere movimiento, la
  página le llega quieta y completa.
