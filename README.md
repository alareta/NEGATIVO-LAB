# Negativo Lab

A single-HTML, offline B&W darkroom for scanned negatives and positives.
No install, no build, no dependencies, no network. Download, double-click, done.

*Un único HTML, offline, para revelar negativos y positivos B&W escaneados.
Sin instalación, sin build, sin dependencias, sin red. Descargar, doble clic, listo.*

---

## English

![Negativo Lab — main view](docs/screenshot-main.jpg)

### What it is

Negativo Lab turns scanned film into finished images, entirely in your browser.
Built as a companion to a basic 8-bit RGB scanner, focused on monochrome work:
B&W negatives, B&W positives, and color negatives processed as B&W.

End-to-end Float32 pipeline. PCHIP-monotone tonal equalizer. Honest sRGB
transfer curves (not γ≈2.2 approximations). TPDF dithered 8-bit output and
optional 16-bit TIFF with Deflate + horizontal predictor — written from
scratch, no external libs.

### How to use

1. Download `negativo_lab.html`.
2. Open it in any modern browser (double-click works).
3. Drag your scan onto the window, or use **Open image**.
4. Pick **Negative** or **Positive** and a sub-mode (see below).
5. Adjust levels, gamma, the 5-zone tonal equalizer, structure and clarity.
6. **Save** as PNG 8-bit (default) or TIFF 16-bit.

For batches: drop several files at once, or open the **Batch** tab. Current
settings are applied to all images.

### Key features

- **Single HTML file.** No install, no build step, no package manager.
  Works offline from `file://`.
- **Float32 pipeline end-to-end.** Inversion, levels, gamma, tonal curve and
  microcontrast all happen in 32-bit float before quantization.
- **Two input types, multiple inversion models.** Negative (linear / sRGB /
  log) and Positive (linear / auto-normalize). Each remembers its last
  sub-mode independently.
- **Eyedropper calibration.** Pick Base+Fog and Dmax directly from the image
  to set the tonal range manually. Live tooltip with linear value and log
  density. Persistent SVG markers.
- **5-zone tonal equalizer with monotone PCHIP interpolation.** Guaranteed
  no tonal inversions, however far you push the sliders.
- **Structure & clarity in perceptual sRGB**, not linear light. Predictable,
  symmetric behavior in shadows and highlights.
- **Honest export.** PNG 8-bit with TPDF dither (default) or 16-bit grayscale
  TIFF with Deflate + horizontal predictor, written by hand without external
  libraries.
- **Batch processing** with a single pipeline pass per image and live
  thumbnails derived from the same Float32 that gets exported.


### Modes at a glance

**Negative:**
- *Linear* — `1−x` in linear light. Attenuator model. Crushes highlights.
- *sRGB* (default) — `1−x` in perceptual sRGB. Sensible compromise.
- *Log* — log-density auto-stretch from the scan's actual range
  (0.5% / 99.5% percentiles). Closest to the photochemical process.

**Positive:**
- *Linear* (default) — no pre-transform. Pure B&W editor.
- *Normalize* — same log auto-stretch, without inversion. Useful for flat
  or underexposed positives.

### Limitations

- Input is 8-bit per channel. The browser's `<img>` quantizes 16-bit PNG/TIFF
  scans on load, so even with a 16-bit source, the effective input is 8-bit.
  The Float32 pipeline still benefits the *output*: TPDF dither breaks
  banding, and the 16-bit TIFF export preserves precision for downstream
  editing.
- B&W only. Color processing is out of scope.
- The UI is currently in Spanish.
- The page loads DM Sans and DM Mono from Google Fonts on first visit. After
  that the browser caches them and the app runs fully offline. If you want
  zero-network from the very first load, delete the `<link>` tag in `<head>`
  and the app will fall back to system fonts.

### License

MIT. See [LICENSE](LICENSE).

---

## Español

![Negativo Lab — vista principal](docs/screenshot-main.png)

### Qué es

Negativo Lab convierte negativos escaneados (o positivos) en imágenes
finales, todo en el navegador. Pensado como complemento a un escáner sencillo
RGB 8-bit, centrado en blanco y negro: negativos B&W, positivos B&W y
negativos color procesados como B&W.

Pipeline Float32 de extremo a extremo. Ecualizador tonal con interpolación
PCHIP monótona. Curvas sRGB reales (no aproximaciones γ≈2.2). Salida 8-bit
con dither TPDF y opción de TIFF 16-bit con Deflate + predictor horizontal —
escrito a mano, sin librerías externas.

### Cómo usarlo

1. Descarga `negativo_lab.html`.
2. Ábrelo en cualquier navegador moderno (doble clic vale).
3. Arrastra tu scan a la ventana, o usa **Abrir imagen**.
4. Elige **Negativo** o **Positivo** y un sub-modo (ver abajo).
5. Ajusta niveles, gamma, el ecualizador tonal de 5 zonas, structure y
   clarity.
6. **Guarda** como PNG 8-bit (por defecto) o TIFF 16-bit.

Para lotes: suelta varios archivos a la vez, o abre la pestaña **Lote**. Los
ajustes actuales se aplican a todas las imágenes.

### Características principales

- **Un único archivo HTML.** Sin instalación, sin build, sin gestor de
  paquetes. Funciona offline desde `file://`.
- **Pipeline Float32 de extremo a extremo.** Inversión, niveles, gamma,
  curva tonal y microcontraste se procesan en coma flotante 32-bit antes de
  la cuantización final.
- **Dos tipos de entrada con varios modelos de inversión.** Negativo
  (lineal / sRGB / log) y Positivo (lineal / auto-normalizar). Cada uno
  recuerda su último sub-modo de forma independiente.
- **Calibración con cuentagotas.** Selecciona Base+Fog y Dmax directamente
  sobre la imagen para fijar el rango tonal manualmente. Tooltip en vivo
  con valor lineal y densidad log. Marcadores SVG persistentes.
- **Ecualizador tonal de 5 zonas con interpolación PCHIP monótona.**
  Garantía: no produce inversiones tonales por mucho que se muevan los
  sliders.
- **Structure y clarity en sRGB perceptual**, no en luz lineal.
  Comportamiento predecible y simétrico en sombras y luces.
- **Exportación honesta.** PNG 8-bit con dither TPDF (por defecto) o TIFF
  grayscale 16-bit con Deflate + predictor horizontal, escrito a mano sin
  dependencias.
- **Procesamiento por lotes** con una sola pasada del pipeline por imagen y
  miniaturas derivadas del mismo Float32 que se exporta.

![Calibración con cuentagotas](docs/screenshot-picker.png)

### Modos de un vistazo

**Negativo:**
- *Lineal* — `1−x` en luz lineal. Modelo atenuador. Aplasta luces.
- *sRGB* (por defecto) — `1−x` en sRGB perceptual. Compromiso razonable.
- *Log* — auto-stretch logarítmico del rango real del scan
  (percentiles 0.5% / 99.5%). El más fiel al proceso fotoquímico.

**Positivo:**
- *Lineal* (por defecto) — sin transformación previa. Editor B&W puro.
- *Normalizar* — el mismo auto-stretch logarítmico, sin invertir. Útil
  para positivos planos o subexpuestos.

### Limitaciones

- La entrada es 8 bits por canal. El `<img>` del navegador cuantiza los PNG
  y TIFF de 16 bits al cargarlos, así que aunque el scan sea de 16 bits, la
  entrada efectiva es 8 bits. El pipeline Float32 sigue beneficiando a la
  *salida*: el dither TPDF rompe el banding, y la exportación TIFF 16-bit
  preserva precisión para edición posterior.
- Solo B&W. El revelado en color queda fuera del alcance del proyecto.
- La página carga DM Sans y DM Mono desde Google Fonts en la primera visita.
  A partir de ahí el navegador las cachea y la app funciona offline al 100%.
  Si quieres cero red desde el primer arranque, borra la etiqueta `<link>`
  del `<head>` y la app caerá a las fuentes del sistema.

### Licencia

MIT. Ver [LICENSE](LICENSE).

