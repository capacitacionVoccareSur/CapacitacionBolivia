# Registro de cambios — capacitacion-bolivia.html

## 23-oct-2026 — Cotizador: reemplazo por web app y archivado de versión Excel

- **Sección 08 reemplazada**: el cotizador basado en Google Sheets (CUADRO COTIZADOR POR CUENTAS_2026.xlsx) fue reemplazado por la web app **Cotizador de Remolques** (Google Apps Script). La nueva sección documenta la interfaz web, los 6 pasos operativos, la generación de PDFs, el correo automático a cabinabo@voccare.global y las reglas de cobro (custodias, IVA).
- **Cotizador v1 archivado**: todo el contenido del cotizador Excel (pestañas, columnas, cuadro interactivo cz-anat, pasos 1-4, tabla de destinos, BISA, errores) fue movido a `<template id="cotizador-v1">`. El template es inerte: no se renderiza ni ejecuta en el navegador, pero el contenido queda preservado en el HTML.
- **Sugerencias (Web3Forms)**: botón flotante "✏ Sugerencias" con modal que envía nombre, sección y mensaje a emorales@voccare.global sin abrir el cliente de correo del usuario.

## 22-oct-2026 — Auditoría Word: reglas faltantes y protocolo Mascotas 123

Cambios surgidos de comparar el "Manual a mano de BOLIVIA.docx" con el HTML actual.

- **Validación Nacional (10 min)**: corregido el tiempo de espera del WPP de Nacional de "5 min" a **10 min**. Si Nacional no responde en 10 min, despachar a riesgo.
- **Dependencia policial**: expandida la tarjeta de condiciones especiales. Se agrega que **el acarreo y el estacionamiento policial no los cubre Nacional Seguros**: el afiliado los paga de su bolsillo.
- **Factor IVA 0,87**: nueva fila en la tabla de errores frecuentes del cotizador. Si el prestador emite factura, multiplicar el costo por 0,87 antes de compararlo con el tope (Addiuva recupera el IVA del 13 %).
- **Custodias**: nueva tarjeta en la sección 08 del cotizador. El costo de custodia se cobra a partir del día 11; los primeros 10 días no generan cargo.
- **Mascotas Ecommerce (123 Asegúrate)**: nueva subsección en Servicios No Viales con protocolo completo: horario L-V 7-20 h, cobertura por ciudades capital, habilitación en 5 días hábiles, tabla de 8 servicios con anticipación requerida y exclusiones clave, regla de excedentes, política de reembolsos y plantilla para escalar a Coordinación Bolivia.

Descartado del Word (no va en el manual):
- Credenciales (6 sets de usuario/contraseña).
- Contenido de Perú (Protecta Security, campaña de salud en S/).
- Contenido de Paraguay (plantillas PY_VIALPROV_*, reembolso Fénix).
- Programa VidaCovid Nacional (pendiente confirmar si sigue activo).
- Porcentaje de Banco Ganadero (pendiente confirmar 20 % vs 40 %).

## 20-oct-2026 (c) — Cotizador: correcciones de contenido

- Pestaña INSPECTORES NACIONAL: texto corregido de "directorio de inspectores de Santa Cruz" a "directorio de inspectores de Nacional Seguros" (aplica a todas las ciudades).
- Cuadro 1 (Cobro excedente interno): descripción actualizada — "Se envía primero al grupo **Coordinación Bolivia**, previa revisión del supervisor, para pedir la autorización de la filial."

## 20-oct-2026 (b) — Cotizador: tabla de 5 columnas réplica exacta del cuadro Excel

- Cuadro cotizador reemplazado: la tabla de 2 columnas fue sustituida por una réplica fiel a 5 columnas del cuadro **COBRO EXCEDENTE INTERNO** de la hoja NACIONAL 2 del `CUADRO COTIZADOR POR CUENTAS_2026.xlsx`.
- Estructura idéntica al Excel: proporciones de columna (37/15/17/14/17 %), `<colgroup>`, merges con `colspan`/`rowspan` incluyendo el `rowspan=2` de "INFORMADO AL CLIENTE POR:" sobre las filas Costo total y Cobertura eje troncal (C20:E21 del Excel).
- Filas: Servicio por · Expediente/Asistencia/Fecha · Asegurado/C.I. · Ciudad/Placa · Dirección del evento · Destino · Inspector · Total km · Km asfalto/ripio · P. unitario asfalto/ripio · Rescate cotizado/oficial · Vehículo pesado · Costo total + INFORMADO (rowspan 2) · Cobertura eje troncal · Cobertura Addiuva/Correo · Cobertura VIP/Teléfono · Cobertura compañía/Operador · Excedente/nombre operador · Orden traslado cliente/proveedor.
- Colores de celda conservados: amarillo `cz-in` (entrada), verde `cz-list` (lista), gris `cz-calc` (calculado).
- Wrapper cambiado de `.grid-2` (50/50) a grid `1fr 260px` para dar espacio a la tabla.
- Datos del ejemplo: 175 km SCZ a 18 Bs/km = 3.150 Bs; AA 700, CC 2.000, NA 450. Sin datos personales del Excel.

## 20-oct-2026 — Auditoría JS/CSS/contenido: bugs, deuda y migración sandbox

- **A1** Bug `--surface-3` indefinida: reemplazado `var(--surface-3)` por `var(--surface-2)` en el hover de sección colapsada.
- **A3** Bug La Paz en cotizador: TARIFAS bisa usaba clave genérica `'La Paz'`; dividida en `'La Paz Altiplano'` y `'La Paz Yungas'` (misma tarifa 20/24 Bs/km). `ciudades[]` eliminó la entrada genérica. La Paz ya no muestra `—` en la tabla.
- **B1** Deuda: eliminada función no-op `updateActiveNav()` y su llamada en el setTimeout del toggle.
- **B2** Deuda: `pct` en CUENTAS ahora se formatea con coma es-BO al renderizar (`'46.8'` → `46,8 %`). Sin cambio en los datos.
- **B3** Deuda: eliminada clase CSS `.placeholder` sin uso en DOM.
- **C** Migración sandbox aprobado: badge `.section-num` sólido verde, `.section-peek` 0.72rem, strips inset por grupo de secciones, KPI hero Total verde (`#panorama-kpis .hero-kpi`), steps más grandes. Añadido `id="panorama-kpis"` y `class="hero-kpi"` al HTML del Panorama.
- **A2** `FB_EMAIL` configurado: `emorales@voccare.global`.

## 15-oct-2026 (i) — Empapelado de marca en tarjetas de sección

- Revisión de diseño con el skill frontend-design: el documento ya tenía identidad propia (verde Bolivia, bento grid, gráficos SVG, mapa interactivo) y no requiere rediseño; se identificaron mejoras puntuales (pendientes: árbol de decisión AA/CC/NA, donut de estados, iconografía de sidebar).
- Se implementó la primera: `--motif`, un rombo andino tenue (SVG inline en data URI, variante light/dark) aplicado como empapelado (`background-repeat: repeat`) en el fondo de cada `.section`, no solo en el header.
- Dos iteraciones previas descartadas por verse demasiado marcadas: (1) rombo escalonado de 26px sin espaciado — parecía malla; (2) rombo simple confinado con `mask-image` solo junto al chevron — se veía parcheado. La versión final cubre toda la tarjeta a opacidad muy baja (0,05 claro / 0,07 oscuro) y tile de 52px, leída como textura ambiental.
- Oculto en `@media print` (`.section { background-image: none !important }`), igual que `.flag-strip`.
- Verificado visualmente en claro y oscuro con un servidor estático temporal + Claude Preview (descartado al terminar).

## 15-oct-2026 (h) — UX: tooltips en gráficos, persistencia de secciones y correcciones de scroll/nav

### Tooltips en gráficos SVG del Panorama
- `svgBarChart()` ahora añade un rect transparente (hit area) por fila que muestra un tooltip flotante (`#bar-tip`) al hacer hover.
- **Familia de servicio**: muestra nombre, desglose por tipo de servicio con cantidades exactas (del Excel, vía Node) y porcentaje del total.
  - Vehicular: Remolque 582 · Auxilio vial 125 · Varios vial 52 · Chofer reemplazo 2
  - Médica: Farmacia 383 · Consultorio 191 · Dental 62 · Análisis clínico 10 · Médico domicilio 3
  - Hogar: Gasfitería 44 · Técnico domicilio 16 · Electricidad 15 · Electrodomésticos 9 · Aire acond. 7
  - Mascota: Asistencia veterinaria 68 · Veterinario en línea 2
  - Telemedicina: Médico en línea 34
  - Otros: Coord. telefónica 7 · Traslado 6 · Funeraria 3 · Siniestros 2
- **Top 10 planes**: muestra nombre del plan, cuenta de origen y porcentaje.
  - Asistencia Vial Nacional → Nacional Seguros · Tu Familia → Alianza Seguros · PRODEM Servicios Médicos → Asist. Nacional Vida y Salud · Medicamentos Banco FIE → Asistencia Banco FIE · EcoHogar → Banco Económico · Sol Integral / Medicamentos BS CSGS → La Boliviana Ciacruz · Mascotas Ecommerce / Familia Protegida JGP → Asist. Nacional Vida y Salud · Asist. p/ Motocicletas → BISA Seguros

### Persistencia del estado de secciones
- El estado abierto/cerrado de cada sección se guarda en `localStorage` (`bolivia-open`: JSON array de IDs).
- Al recargar la página, las secciones que estaban abiertas se restauran automáticamente (incluyendo el gráfico del panorama si estaba activo).

### Subtítulos visibles en cards comprimidas
- Se añadió `.section-peek` (p) entre el h2 y el `.section-body-wrap` en las 10 secciones.
- CSS: `[aria-expanded="true"] + .section-peek { display: none }` — desaparece al expandir, sin JS.

### Correcciones de espaciado y navegación
- `#main { padding-top: 16px }` — evita que la primera sección quede pegada al borde inferior del header fijo.
- `scroll-margin-top` actualizado a `calc(var(--header-h) + 16px)`.

### Comportamiento del sidebar y nav activo
- Clic en sidebar ahora hace **toggle** (abre si está cerrado, cierra si está abierto).
- `e.preventDefault()` en sidebar: evita el scroll nativo del anchor, dejando solo el `scrollIntoView` del toggle.
- `navFrozen` se activa tanto desde el sidebar (700 ms) como desde el toggle handler (900 ms), evitando que el IntersectionObserver / scroll listener actualice el nav durante la animación.
- **Scroll tracking eliminado**: el `IntersectionObserver` y el listener `scroll` se removieron para evitar el recorrido no deseado del nav. El nav activo sólo cambia al hacer clic en el sidebar.

## 15-oct-2026 (g) — Sección 08 Cuadro Cotizador

- **Nueva sección 08 "Cuadro Cotizador"** (`#cotizador`), después de Tipificación. Reembolsos y Farmacias pasa a **09** y Errores y Terminología a **10**.
- **Fuente**: `CUADRO COTIZADOR POR CUENTAS_2026.xlsx`, exportado de Google Sheets. Pestañas visibles: NACIONAL 1, 2 y 3, VIP BANCO PRODEM, BISA 1504, BANCOS – NACIONAL e INSPECTORES NACIONAL. Las demás están ocultas.
- **Confirmado por el usuario**:
  - En el cuadro, la cobertura de Addiuva es AA, la de la compañía es CC y el excedente del cliente es NA.
  - Las tarifas de Yungas varían por cuenta.
  - La maniobra se cotiza con el proveedor a partir de una foto del vehículo y se cobra aparte.
  - NACIONAL 1, 2 y 3 existen para que no se pisen solicitudes en paralelo.
- **Contenido**:
  1. Elegir la pestaña según la cuenta, con los bancos con póliza colectiva y los clientes con cobertura especial (Prodem, YPFB, Gas Transboliviano).
  2. Elegir la columna según la ciudad.
  3. Completar el cuadro: réplica con colores (lista, escribir, calculado) y una explicación por fila al pasar el mouse.
  4. Destino de cada uno de los 3 cuadros y lo que lleva el correo de notificación de excedente.
  5. Simulador, tabla de tarifas y errores frecuentes.
- **Fidelidad del simulador**:
  - Usa los precios que cada pestaña calcula de verdad. NACIONAL 1, 2 y 3 leen la tabla de la pestaña NACIONAL 2 (Yungas ripio 26). La tabla visible de NACIONAL 1 dice 32, pero no se usa. VIP usa su propia tabla (Yungas 28).
  - Recargos: maniobra +30 % (BISA +29 %), cotización del proveedor +15 %.
  - Tiene 4 autocontroles (`console.assert`) con casos reales de la hoja: eje troncal, resto del país con siniestro, VIP y BISA.
- **No se usan datos reales** del libro (asegurados, placas, teléfonos de inspectores). El ejemplo es ficticio.
- **Pendientes**:
  - Definir qué son M2 y M3 en BISA.
  - NACIONAL 3 recarga 35 % (maniobra y cotización), distinto de las otras pestañas. El simulador usa 30 % y 15 %.
  - En BISA, la tabla por departamento (km y Bs) no coincide con la fórmula, que usa solo la categoría. El simulador sigue la fórmula.
  - En BISA, el excedente puede salir negativo en la hoja; el simulador lo muestra como 0.
- **Arreglo de un error de la migración (f)**: `let panoramaChartsDrawn` se leía en `setTheme()` antes de declararse. El error cortaba el script al cargar (tema, secciones colapsables, parallax). Se cambió a `var`.

## 15-oct-2026 (f) — Migración del sandbox al principal

- **Chart.js eliminado** (~300 KB): las dos canvas del panorama se reemplazaron por `<div>` y gráficos SVG puros (sin dependencia externa). El archivo sigue funcionando sin conexión.
- **Secciones como tarjetas**: `.section` cambia de separador `border-bottom` a carta con `border: 1px solid`, `border-radius: 20px`, `background: var(--surface)`. Márgenes: `margin-bottom: 16px`.
- **Bento grid** añadido: `.bento` 6 columnas con clases `.c1`–`.c6`. El panorama usa una tira de 6×c1 (KPIs) y una fila c2 + c4 (gráficos). Responsive: 3 cols a 900 px, 2 cols a 600 px.
- **Colapso suave** (grid-row trick): cada cuerpo de sección queda envuelto en `.section-body-wrap > .section-body-inner`. El JS añade/quita `.open` en vez de `style.display`. Transición 0,38 s cúbica.
- **Stagger de tarjetas**: al abrir una sección las tarjetas animan de abajo a arriba con un retraso escalonado de 50 ms (`animation-delay: calc(var(--i,0) * 50ms)`).
- **Parallax marcas de agua**: `::before` de cada `.section` muestra el número de sección (CSS counter) con `font-size: 9rem` y `opacity: 0.05`. El JS mueve `--par` en scroll (`getBoundingClientRect().top * 0.35`).
- **Gráficos panorama (SVG vanilla)**: `svgBarChart()` dibuja barras horizontales con pista, etiqueta y valor. `chart-familias` (ml 110) y `chart-planes` (ml 175) se renderizan al abrir el panorama y se redesetean al cambiar de tema.
- El `sandbox-redesign.html` queda intacto para pruebas futuras.

## 15-oct-2026 (e) — Mapa por regiones, tabla corregida e interacción

- Subsección renombrada a **"Departamentos y regiones"**. El mapa se colorea por región: **Occidente** (La Paz, Oruro, Potosí), **Valles** (Cochabamba, Chuquisaca, Tarija) y **Oriente** (Santa Cruz, Beni, Pando). El código de área queda como dato secundario, porque coincide con la región (2, 4 y 3).
- Nueva tarjeta **"Cómo se habla de las regiones"**: altiplano, "el centro" (Cochabamba), "el sur", llanos, Amazonía, Chaco, eje troncal y gentilicios. "Colla" y "camba" se marcan como coloquiales, para no usarlos con el afiliado.
- **Tabla corregida**:
  - Camiri pasa de Chuquisaca a **Santa Cruz** (provincia Cordillera).
  - Chuquisaca: Monteagudo y Camargo.
  - Pando: Porvenir (antes "—").
  - Se completaron más ciudades: Caranavi, Challapata, Villazón, Tupiza, Bermejo, Villamontes y Guayaramerín.
  - La capital de Santa Cruz figura como "Santa Cruz de la Sierra".
  - La tabla se ordena por región y tiene una nueva columna Región.
- **Interacción**:
  - Hover o foco sobre un departamento: se resalta con contorno, se atenúan los demás, se marca su fila en la tabla y un recuadro muestra región, código, capital y ciudades.
  - Funciona también al revés, desde la fila de la tabla.
  - Clic o toque fija la selección (útil en celular); otro clic o Escape la quita.
  - Los botones de región resaltan sus tres departamentos.
  - Navegable con teclado (Tab, Enter).

- Sección 02, "Departamentos y prefijos": la silueta dibujada a mano se reemplazó por los **9 departamentos con sus límites reales**. Fuente: geoBoundaries BOL ADM1 (derivado de GeoBolivia, dominio público), proyectado y simplificado a unos 12 KB de SVG embebido. Funciona sin conexión.
- Cada departamento se pinta con el color de su código de área (2 azul, 3 ámbar, 4 verde). Las 9 capitales van en su ubicación real. Al pasar el mouse sobre un departamento se muestra su nombre y su código.
- Los huecos blancos en Potosí y Oruro son los salares de Uyuni y Coipasa, que vienen así en la fuente.
- Se quitaron las elipses de región (Altiplano, Valles, Oriente, Amazonía) y las líneas divisorias de prefijo.
- El rediseño Bento (15-oct (c)) vive en `sandbox-redesign.html`. Al pasarlo al manual hay que conservar este bloque del mapa.

## 15-oct-2026 (c) — Rediseño Bento Grid

- **Base font**: 16px (antes 14px). Sistema: `Segoe UI Variable Display/Text` en Win11, `SF Pro` en macOS. `font-optical-sizing: auto`, `-webkit-font-smoothing: antialiased`.
- **Border-radius**: 20px / 12px / 28px (tokens `--radius` / `--radius-sm` / `--radius-lg`). Antes: 12px / 8px.
- **Cards**: borde completo `1px solid var(--border)` (antes asimétrico), `padding: 20px 24px` (antes 12px 14px), sombra rediseñada con ring + blur.
- **KPI values**: `2.8rem, font-weight: 800, letter-spacing: -0.04em` (antes 1.6rem 700).
- **Section titles**: `1.65rem, font-weight: 800, letter-spacing: -0.04em` (antes 1.18rem). Sin `border-left`. `.section-num` como etiqueta discreta con border.
- **Grids**: gap 16px (antes 10px). Nuevo `.bento` con `auto-fit` y soporte `.span-2`.
- **Toggle chevron**: convertido en pill circular con fondo `surface-2` y borde.
- **Responsive**: `.section { padding: 28px 20px }` y `font-size: 1.3rem` bajo 900px.

## 15-oct-2026 (b) — DOKKA y alineación de la documentación

- **DOKKA**: el usuario confirmó que las solicitudes viales que llegan por DOKKA son **exclusivas de Nacional**. Sección 06, tarjeta "Recibir solicitudes viales": se indica que ninguna otra cuenta usa ese canal. Se cierra el pendiente del 14-oct (c).
- **plan.md** alineado con este registro: base de 1.642, cifras de T2, top 10 con Banco Fortaleza en lugar de IKATECH, filtros por familia con Mascota y sin Mixta, fila DOKKA, tabla de farmacias (10 cuentas, 383), nueva tarea T5b Servicios No Viales y decisiones de diseño (tema según el sistema, sin credenciales, terminología, numeración de secciones).
- **todo.md**: filtros de cuentas marcado como hecho (se hizo el 14-oct (b)); añadidos T5b y las secciones colapsables.
- Nuevo `CLAUDE.md` con la estructura del HTML, las fuentes de datos y las convenciones.

## 15-oct-2026 — Secciones colapsables

- Las 9 secciones son ahora desplegables: clic en el `h2` colapsa/expande el cuerpo.
- El chevron (▲) rota al colapsar; el patrón es idéntico al que ya tenía la sección 01.
- El nav lateral auto-expande la sección destino si está colapsada al hacer clic en el enlace.

## 14-oct-2026 (c) — Reglas por cuenta y terminología

- **"Subcuenta" → "plan"** en todo el manual y en plan.md (error del pptx). En plan.md también se quitaron los "sponsor" que quedaban.
- **Servicios No Viales**: el dato crítico es la **foto del daño reportado**, no de la fachada.
- **Reglas por cuenta** (pptx, diap. 08) añadidas a las tarjetas del top 10:
  - Nacional: los planes Hogar (Casa Protegida, Coop. Jesús Nazareno) se validan por SOA.
  - Alianza: si el portal falla, escalar de inmediato al grupo filial de WhatsApp de Alianza.
  - BISA (Motos): no se valida la vigencia tradicional; revisar el historial de reincidencias del día.
  - Asist. Nacional Vida y Salud: se reemplazó "Vida vs Salud" (no existe) por los planes reales.
- **Descuento farmacia** (sección 08, paso 1): si el registro falla, escalar al supervisor indicando la antigüedad del afiliado.
- ~~**Pendiente**: confirmar si las solicitudes viales que llegan por DOKKA son solo de Nacional.~~ Confirmado el 15-oct-2026: son exclusivas de Nacional.
- **Top 10 Cuentas**: cada tarjeta muestra como subtítulo sus planes, con volumen, según el Excel (hasta 3 y "+N más"). Los datos completos están en `planes` de cada cuenta.

## 14-oct-2026 (b) — Hogar, DOKKA, despacho de grúas y servicios no viales

- **Renumeración**: nueva sección **05 Servicios No Viales** (`#no-vial`). Plataformas pasa a 06, Tipificación a 07, Reembolsos y Farmacias a 08 y Errores y Terminología a 09. Las referencias de las entradas anteriores de este registro usan la numeración vieja.
- **Top 10 Cuentas**:
  - Cada cuenta lleva `familias` (familias con 5 o más asistencias, según el Excel) y aparece en cada filtro donde tiene servicios.
  - Filtros: Todas / Vehicular / Médica / Hogar / Mascota, con conteo y `aria-pressed`. Se quitó el filtro "Mixta".
  - **Hogar** (4 cuentas): Nacional Patrimoniales 38, Banco Económico 37, La Boliviana 15, Asist. Nacional Vida y Salud 7. Fuera del top 10, La Promotora EFV tiene 4.
- **DOKKA** (sección 06):
  - Es la ticketera de Nacional y sirve para dos cosas: **recibir solicitudes viales** y derivar o escalar casos (incluidos los siniestros).
  - Se añadieron los 4 datos, la ruta de registro, el speech, el seguimiento (el creador es el responsable) y el cierre (Addiuva cierra solo la etapa de asistencia).
- **Despacho de grúas** (sección 04): registro técnico obligatorio, canal oficial de WhatsApp, tiempos (ETA del proveedor de menos de 10 min y TEA de 15 o 10 min), condiciones especiales (siniestrado, dependencia policial, sótano) y responsabilidades de Addiuva y de Full Assistance.
- **Servicios No Viales** (sección 05): validación SOA, datos críticos, beneficiarios, video-validación, protocolo medidor, aire acondicionado, servicios personales, eventos y especiales, y rutina diaria. La regla de siniestros es la del usuario, que reemplaza el "NO coordinar" del pptx.

## 14-oct-2026 — Correcciones tras la auditoría de contenido

### Reglas confirmadas por el usuario
- Se excluyen de todas las cifras las cuentas **IKATECH** (prueba, 14 asistencias) y **Addiuva Enterprises** (interna, 5).
- **Farmacia**: "Cancelado posterior" es su cierre normal, no una cancelación.
- **Siniestros**: no somos cabina de siniestros. Los de Nacional se derivan por DOKKA. Los servicios derivados de un siniestro solo se coordinan con aval de la cuenta.
- **30 km**: recorrido mínimo cubierto en zona urbana. De 30 a 150 km se usa el cuadro cotizador para calcular el excedente (NA). El cuadro cotizador está pendiente de que lo comparta el usuario.
- **TEA**: 15 min para todas las cuentas, 10 min para BISA.

### Cifras recalculadas (base 1-ago a 12-oct-2026, sin IKATECH ni Addiuva)
| Métrica | Antes | Ahora |
|---|---|---|
| Asistencias | 1,661 | 1.642 |
| Concluidas | 805 (48.5 %) | 804 (49,0 %) |
| Canceladas | 744 (44.8 %) | 726 (44,2 %), de ellas 382 son cierres de farmacia |
| En proceso | 112 (6.7 %) | 112 (6,8 %) |
| Cuentas activas | 10 | 17 |
| Proveedores | 15+ | 93 |
| Familias | 765/659/101/70/34/32 | 761/658/101/70/34/18 |
| Estados | 805/498/246/112 | 804/486/240/112 |

- Alerta de Panorama reescrita: sin farmacia, la cancelación es del 27,3 % (344 de 1.259).
- % del top 10 recalculados sobre 1.642. Banco Fortaleza queda como #10 de forma legítima.
- Proveedores: V.H. Cronenbold pasa a 50 y "Grúas" (antes "Médico"); Arce Motors a 31. Los % se calculan sobre `TOTAL_ASIST`.
- Tabla de farmacias completa: 10 cuentas y 383 asistencias, con % sobre 383. Se añadieron Banco Fortaleza, Sagrada Familia, Fortaleza Seguros y CIDRE.
- Nueva subsección **TEA** en la sección 05.
- Textos de siniestros (secciones 05 y 08) y de cotizador o 30 km (secciones 04, 05, 06 y 08) alineados con las reglas.
- Constante `TOTAL_ASIST = 1642` en `<head>`, usada por gráficos y proveedores.

### Fuentes
- "Información Bolivia.xlsx", hoja Dashboard: **no es fiable**. Sus fórmulas nativas terminan en la fila 1000 (cuentan 999 de 1.661), mientras que las de Google Sheets conservan valores de la base completa. `Sheet1` sí es la misma base que el Excel de transferencias.

## 13-oct-2026

### Navegación y móvil
- Botón ☰ en el header bajo 900px: abre la barra lateral; se cierra al tocar fuera, al elegir una sección o con Esc.
- Las secciones tienen `scroll-margin-top`, así el header fijo ya no tapa el título al saltar desde el índice.
- Las tablas se desplazan en horizontal en vez de recortarse. En móvil, el padding de las secciones baja a 16px y se oculta la metadata del header.

### Pasos numerados
- Se quitaron los `.step-num` que duplicaban el número (secciones 05 y 07). El título y el cuerpo van ahora dentro de un `<div>`, igual que en la sección 02.
- El flujo de cierre (SOA → CallBell → Vicidial) usa `.steps.flow`: en horizontal en escritorio y apilado en móvil.

### Accesibilidad
- Título del header en `<h1>` y títulos de sección en `<h2>`.
- Foco visible global (`:focus-visible`) y `<label>` oculto en el buscador.
- Contrastes corregidos: código AA, badges Médica y Hogar, números del menú y `--text-muted` en modo oscuro (`#8FB394`).
- El botón de tema muestra la acción (☾ / ☀) y actualiza su `aria-label`.
- Los gráficos llevan `role="img"` y un `aria-label` con los datos.

### Colores
- Tokens nuevos en `:root` y en `[data-theme="dark"]`:
  - `--fam-*`: vehicular, medica, hogar, mascota, telemedicina, mixta, otros
  - `--st-*`: concluida, canc-post, canc-mom, proceso
  - `--code-aa`
- Gráficos, badges de cuentas y tabla de proveedores usan los mismos tokens. "Reembolso" en proveedores pasa a gris neutro.
- Se eliminaron las clases `.badge-*`, que no se usaban.

### Gráficos
- Chart.js 4.4.0 va embebido (ya no depende de jsDelivr).
- `refreshCharts()` recolorea los gráficos al cambiar de tema.
- Si Chart.js no carga, los datos se muestran como lista.
- Los tooltips usan formato es-BO.

### Contenido
- Sección 02: se eliminó la tabla de prefijos de 3 columnas, que estaba duplicada. Queda la de 4 columnas junto al mapa, y los datos obligatorios ocupan todo el ancho.
- Sección 06: definiciones AA/CC/NA, árbol de decisión y caso práctico reescritos con las definiciones del usuario. El cierre de farmacia (sección 07) y la tabla de errores (sección 08) se ajustaron igual.
- "Sponsor" se reemplazó por "cuenta" en reembolsos.
- Semáforo de estados SOA: descartado.

### Pendiente de validar
- Ejemplos de CC (excepciones autorizadas por la cuenta): confirmar con operaciones que reflejan casos reales.
