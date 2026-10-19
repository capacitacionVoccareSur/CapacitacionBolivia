# Todo — Documento Capacitación Bolivia

## Fase 1: Estructura
- [x] T1 — Scaffold HTML base (nav, estilos, Chart.js inline, secciones vacías)
  - Chart.js quedó embebido el 13-oct-2026; antes se cargaba por CDN
  - CP1: Revisión de diseño con usuario antes de continuar

## Fase 2: Secciones de datos (paralelas)
- [x] T2 — Panorama de la Operación (KPIs + gráficos del Excel)
- [x] T3 — Sistema SOA y Datos Obligatorios (checklist + mapa + jerarquía)
  - Semáforo de estados SOA descartado por el usuario
- [x] T4 — Top 10 Cuentas (cards filtrable + rutas de validación)
- [x] T5 — Proveedores Clave (tabla top 15 + Full Assistance tarifas + farmacias)
- [x] T5b — Servicios No Viales (sección 05: validación SOA, foto del daño, medidor, servicios personales, TEA)
  - CP2: Revisión de cobertura de datos ← PENDIENTE usuario

## Fase 3: Secciones de protocolo (paralelas)
- [x] T6 — Plataformas y Sistemas (tabla + flujo cierre + reglas DOKKA)
- [x] T7 — Tipificación Financiera AA / CC / NA (árbol de decisión + caso práctico)
  - Definiciones corregidas por el usuario el 13-oct-2026 (ver plan.md, T7)
- [x] T8 — Reembolsos y Módulo Farmacias (flujos numerados + tabla cuentas farmacia)
- [x] T9 — Errores Frecuentes y Terminología Local (tabla 5 errores + glosario 16 términos)
  - CP3: Revisión de exactitud de protocolos ← PENDIENTE usuario

## Fase 3b: Mejoras UX (revisión de diseño del 13-oct-2026)
- [x] Pasos numerados arreglados (secciones 05 y 07)
- [x] Menú móvil (☰) y desbordes en pantallas pequeñas
- [x] `scroll-margin-top` para que el header no tape los títulos
- [x] Contrastes WCAG AA, foco visible, `h1`/`h2`, label en buscador
- [x] Colores unificados por familia de servicio y por estado (tokens CSS)
- [x] Gráficos que cambian con el tema y respaldo si Chart.js no carga
- [x] Tabla de prefijos duplicada eliminada
- [ ] Escala tipográfica: base 16px, mínimo 12px (hoy hay textos de 9–10px)
- [ ] Pasar los estilos inline (~295) a clases reutilizables
- [ ] Buscador que busque dentro del contenido, no solo en el menú
- [x] Filtros de cuentas: conteo por familia y cuentas mixtas en todas sus familias (14-oct-2026)
- [x] Secciones colapsables con clic en el título (15-oct-2026)
- [ ] Formato de números es-BO en los textos (1.642 · 49,0 %). Ej.: el campo `pct` de `CUENTAS` usa punto ('46.8')
- [ ] Unificar el nombre del manual (hoy hay tres variantes)
- [ ] Decidir qué hacer con `dashboard.html` (archivar o alinear estilos)

## Fase 4: Cierre
- [ ] T10 — Polish: CSS print/PDF, búsqueda, tabla de contenidos, pie de página
  - Hecho: leyenda de gráficos en modo oscuro
  - Falta: print con tema claro forzado, pie con fecha y fuente, botón Imprimir/PDF
  - CP5: Revisión final go/no-go
