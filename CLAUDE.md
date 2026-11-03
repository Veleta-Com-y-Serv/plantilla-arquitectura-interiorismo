# Plantilla «Arquitectura e interiorismo» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **minimal**, a ancho completo.
Todo en castellano de España, frases cortas, sin jerga. El brief de diseño está en `DISEÑO.md`.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = bandas oscuras y pie, acento = terracota de bandas, botones y números, fondo = blanco, texto = tinta). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…) y Tailwind los expone como `bg-primario`, `text-acento`… Los derivados (líneas, gris del texto, papel milimetrado) salen con `color-mix` en `src/styles/global.css`.
- **Tipografías y aspecto general**: `src/styles/global.css` (sans ligera del sistema para títulos, antetítulos en mayúsculas espaciadas con línea de acento, bandas `.banda-clara/.banda-papel/.banda-oscura/.banda-acento`, botones `.btn`/`.btn-sec`, cabecera, pie, mosaico). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Las fotos van en `public/fotos/` (se generan a partir de `fotos.json`); los SVG de respaldo están en `public/placeholders/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/portada.jpg`). Las personas del equipo usan `/placeholders/persona.svg` hasta que el cliente sube su foto.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = inicial en un cuadro + nombre en texto.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`, en el orden de `site.yaml`. Todas son bandas a todo el ancho.
- `hero` → `hero.astro`: portada a pantalla completa con foto a sangre, título enorme, dos botones (`cta`, `cta_secundario`) y línea de cota con la localidad.
- `proyectos` → `proyectos.astro`: mosaico asimétrico de borde a borde; `proyectos[]` {titulo, texto, lugar, anio, imagen, categoria}. Filtro por `categoria` si hay dos o más.
- `manifiesto` → `manifiesto.astro`: banda de acento con la frase (`texto`) y su firma (`autor`). Sin frase no se pinta.
- `sobre-nosotros` → `sobre-nosotros.astro`: «El estudio», foto a sangre 50/50 + texto y el equipo (`personas[]` {nombre, cargo, foto, texto}).
- `servicios` → `servicios.astro`: banda oscura con franja de fichas de borde a borde; `items[]` {titulo, texto, imagen} y `cta`.
- `proceso` → `proceso.astro`: papel milimetrado y línea de tiempo; `items[]` {titulo, texto, duracion}.
- `premios` → `premios.astro`: banda oscura con filas por año; `items[]` {titulo, texto, anio}.
- `preguntas` → `preguntas.astro`: acordeón `details/summary`; sin preguntas no se pinta.
- `cta` → `cta.astro`: banda con foto a sangre y velo; `cta` y `cta_secundario`.
- `contacto` → `contacto.astro`: banda partida (datos sobre el fondo, formulario sobre el acento hasta el borde).
- `texto` → `texto.astro`: diseño genérico para apartados nuevos (`tipo: texto`), con foto a sangre 50/50 si la tiene.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`. Mantén la alternancia de bandas (clara, oscura, acento) si puedes.
3. **Cambiar textos, teléfonos, horarios, fotos**: solo en `site.yaml`. Si un texto contiene comas o «: » dentro de `{ … }`, ponlo entre comillas. Precios siempre entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista; máximo 24 elementos por lista.
5. **Página nueva**: crea `src/pages/<slug>.astro` con `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro` (empieza por una banda oscura; la cabecera fija deja sitio sola).
6. **Sección nueva**: crea `src/components/secciones/<id>.astro` (copia la estructura de una existente: `seccion(id)`, `Seccion` con su `banda`, `Titular`) y añade `secciones.<id>` en `site.yaml`. `src/pages/index.astro` la recoge sola.
7. **No tocar** `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt) y salen solos de `site.yaml`. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), JavaScript solo el pequeño en línea que hay (cabecera y filtro de proyectos), 16 px de margen lateral (`.contenedor`), fotos y fondos de borde a borde, sin scroll horizontal en móvil, botones de 44 px de alto o más. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""`.
9. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Campos propios de esta plantilla (además del esquema común)
- `proyectos.proyectos[]`: {titulo, texto, lugar, anio, imagen, categoria}.
- `manifiesto`: `texto` (la frase) y `autor`.
- `servicios.items[]`: {titulo, texto, imagen}; `proceso.items[]`: {titulo, texto, duracion}; `premios.items[]`: {titulo, texto, anio}.
- `hero.cta_secundario` y `cta.cta_secundario`: segundo botón.

## Páginas propias (fichas por elemento)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): `secciones.proyectos.proyectos` → `/proyectos/<slug>/` (proyecto).
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (precio, duración…) salen en la tabla de datos de la ficha.
- Una orden «añade una página para X» = escribir su `detalle` en site.yaml. Nunca crees a mano páginas en
  `src/pages/proyectos/`: salen solas de `src/pages/[coleccion]/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y servicio/producto con precio si lo hay).

## Varias páginas
- `paginas:` (raíz de site.yaml, opcional): `[{ ruta, titulo, secciones: "servicios; planes" }]`, como mucho 6, cada sección en una sola página y nunca `hero`. Con ella la web pasa a Inicio (hero + lo que no esté en ninguna página) y una página por entrada (`/servicios/`…); el menú se hace solo con las páginas (las entradas `/#…` de `menu` no salen) y los enlaces `/#id` del site.yaml se cambian solos por la dirección de su sección. Sin ella, una sola página larga. Una orden «haz la web de varias páginas» = escribir `paginas`; nunca crees páginas a mano para eso.
- No tocar `src/lib/multipagina.ts`, `src/pages/index.astro` ni `src/pages/[...pagina].astro` (comunes a todas las plantillas). En un componente, un enlace fijo a una sección va con `enlace('/#contacto')` (de `src/lib/multipagina.ts`).
