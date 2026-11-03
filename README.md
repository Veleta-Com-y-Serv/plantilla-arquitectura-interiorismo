# Plantilla NoExpertise · Arquitectura e interiorismo

Web a ancho completo para estudios de arquitectura e interiorismo, con proyectos en mosaico a sangre.

- Sectores: arquitectura, interiorismo, decoración, estudio de diseño, paisajismo. Estilo: minimal. Plan mínimo: presencia.
- Secciones: hero, proyectos, manifiesto, sobre-nosotros, servicios, proceso, premios, preguntas, cta, contacto (y `texto` para apartados nuevos).
- Ejemplo: Arraiz Estudio, estudio ficticio de Bilbao.
- Concepto y paleta en `DISEÑO.md`; contenido en `site.yaml`; metadatos y guion del asistente en `template.yaml`; fotos a generar en `fotos.json`; reglas para el agente en `CLAUDE.md`.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Varias páginas (opcional, `paginas:` en la raíz de `site.yaml`): Inicio + una página por entrada (`{ ruta, titulo, secciones: "a; b" }`, hasta 6) con el menú hecho solo; reparto recomendado en `template.yaml → paginas`. Sin la clave, una sola página larga.

## Campos propios

| Sección | Lista | Campos |
|---|---|---|
| `proyectos` | `proyectos` | titulo, texto, lugar, anio, imagen, categoria (filtro) |
| `manifiesto` | — | texto (la frase), autor |
| `sobre-nosotros` | `personas` | nombre, cargo, foto, texto |
| `servicios` | `items` | titulo, texto, imagen |
| `proceso` | `items` | titulo, texto, duracion |
| `premios` | `items` | titulo, texto, anio |
| `hero`, `cta` | — | cta, cta_secundario |

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de respaldo (`public/placeholders/`) hechas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.proyectos.proyectos` con `detalle` tiene su página en `/proyectos/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
