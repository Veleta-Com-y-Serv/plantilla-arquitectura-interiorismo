# Arquitectura e interiorismo: brief de diseño

Plantilla `arquitectura-interiorismo` creada el 29/10/2026 a partir de `portfolio` con `php artisan plantillas:nueva`
y rediseñada entera (tanda «ancho completo», fila 4). Este fichero se queda en el repo: es lo que lee quien
(persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: estudios de arquitectura, interiorismo, decoración, diseño y paisajismo (`sectores`). Su cliente
  entra a ver obra: quiere fotos grandes, saber cómo se trabaja y pedir una visita.
- **Qué tiene que conseguir la web**: que el visitante pida una primera visita (botón de la cabecera, banda final
  y formulario) después de ver los proyectos.
- **Tono y estilo** (`minimal`): sereno, preciso, luminoso. Sí: revistas de arquitectura, láminas de proyecto con
  cotas y retícula. No: la caja centrada estrecha con tarjetas blancas ni la rejilla de filetes y monoespaciada de
  `portfolio`.
- **Concepto «planta y sección»**: la web se lee como un juego de planos. Bandas a sangre que alternan blanco,
  tinta y terracota; fotos de borde a borde; detalles de dibujo técnico (línea de cota con topes, retícula de
  columnas sobre las bandas oscuras, papel milimetrado en el proceso, cuadrito de acento como marca de nivel).
- **Paleta de ejemplo**: primario `#161514` (tinta: bandas oscuras y pie), acento `#b4532f` (terracota: banda del
  manifiesto, mitad del contacto, botones, números), fondo `#ffffff`, texto `#161514`. Derivados con `color-mix`
  (líneas al 14 %, gris de texto, papel al 4 %): aguanta cualquier combinación del cliente con buen contraste
  entre fondo y texto, y acento y fondo.
- **Tipografía**: del sistema. Títulos en sans ligera (peso 200, «Segoe UI Variable Display» / «Helvetica Neue»)
  muy grande (hasta 7,75 rem en la portada, 3 rem en móvil) con interletrado negativo; antetítulos y botones en
  mayúsculas pequeñas con interletrado ancho; números de orden en la misma sans ligera, en acento.
- **Ritmo de bandas** (de arriba abajo): portada foto a sangre 100 svh → proyectos blanco con mosaico de borde a
  borde → manifiesto terracota → estudio blanco con foto a sangre 50/50 y equipo → servicios tinta con franja de
  fotos → proceso papel milimetrado → premios tinta → preguntas blanco → llamada foto a sangre con velo →
  contacto partido blanco/terracota → pie tinta con la firma enorme del nombre.

## Apartados

| id | Banda | Qué enseña | Lista propia |
|---|---|---|---|
| `hero` | foto a sangre | título enorme, entradilla, dos botones, cota con la localidad | — |
| `proyectos` | clara | mosaico asimétrico de 6 columnas (grande, dos pequeñas, alta, dos apaisadas) sin márgenes; filtro por categoría | `proyectos`: titulo, texto, lugar, anio, imagen, categoria |
| `manifiesto` | acento | una frase enorme y su firma | — (`texto`, `autor`) |
| `sobre-nosotros` | clara | foto a sangre 50/50 + historia; equipo en 4 columnas en blanco y negro | `personas`: nombre, cargo, foto, texto |
| `servicios` | oscura | franja de fichas de borde a borde con foto, número, título y texto | `items`: titulo, texto, imagen |
| `proceso` | papel | línea de tiempo horizontal (vertical en móvil) | `items`: titulo, texto, duracion |
| `premios` | oscura | filas con el año enorme en acento | `items`: titulo, texto, anio |
| `preguntas` | clara | titular a la izquierda, acordeón a la derecha | `preguntas` |
| `cta` | foto a sangre | título enorme y dos botones | — |
| `contacto` | clara + acento | correo enorme y datos; formulario `mailto` sobre el acento | — |
| `texto` | clara | genérico; foto a sangre 50/50 si la tiene | `items` |

## Fotos

`fotos.json` (13): portada (salón de un piso del Ensanche con mirador), seis proyectos (cocina de piso señorial,
caserío, casa frente al mar, cafetería, oficina en nave, ático bajo cubierta), mesa del estudio, cuatro servicios
(reforma en curso, piedra y madera de un caserío, muestras de materiales, tienda reformada) y la galería
acristalada de la banda final. Luz natural del norte, encuadres de fotografía de arquitectura, sin gente, sin
texto ni logotipos. Las personas del equipo usan `/placeholders/persona.svg`.

## Qué no hacer

- Volver a la columna estrecha con tarjetas o al índice de filetes con monoespaciada de `portfolio`.
- Márgenes alrededor del mosaico o de la franja de servicios: tocan los bordes de la ventana.
- Cifras o precios fijos en los componentes (solo en `site.yaml`).
- Más de un color saturado: el acento es uno y se usa en bandas enteras, botones y números.
