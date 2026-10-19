# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Qué es este proyecto

Manual de capacitación operativa de Addiuva Bolivia para coordinadores y cabinas. El entregable es un único archivo HTML autocontenido, `capacitacion-bolivia.html`, que sirve como referencia diaria y como material de presentación. No hay build, ni tests, ni repositorio git. Se verifica abriendo el archivo en el navegador (sin conexión) y con Ctrl+P para la versión impresa. No abras archivos con `start`: el usuario los abre.

- `tasks/plan.md`: plan de tareas T1–T10 con criterios de aceptación.
- `tasks/todo.md`: estado actual y pendientes.
- `tasks/cambios.md`: registro de cambios y reglas confirmadas por el usuario. Añade una entrada fechada cada vez que cambies contenido o cifras. Formato del encabezado: `## DD-mmm-YYYY (letra) — descripción breve` (la letra distingue varias entregas del mismo día, empezando por `b` si ya existe una entrada sin letra).
- `dashboard.html`: dashboard de análisis anterior. No se mantiene; su destino está pendiente (ver todo.md).
- `sandbox-redesign.html`: banco de pruebas para cambios visuales. Úsalo para probar rediseños antes de migrar al principal. No lo borres.

## Arquitectura de `capacitacion-bolivia.html`

- **Sin dependencias externas**: todo el CSS en un `<style>`, JS inline y la constante `TOTAL_ASIST` (base de todos los porcentajes) en `<head>`. Debe funcionar sin red: no usar CDN.
- **CSS**: tokens en `:root` y en `[data-theme="dark"]`. Los colores de familia de servicio (`--fam-*`) y de estado (`--st-*`) son tokens compartidos por las tarjetas y los gráficos. AA/CC/NA usan `--code-aa`, `--accent` y `--gold`. Hay un bloque `@media print`.
- **Secciones**: `<section class="section" id="...">` numeradas 01–10 (panorama, soa, cuentas, proveedores, no-vial, plataformas, tipificacion, cotizador, reembolsos, errores). Cada una tiene un `h2.section-toggle` con `data-target` y un cuerpo `.section-body-wrap > .section-body-inner` (colapsable, se abre con la clase `.open`). El menú lateral enlaza a estos ids. Si renumeras, actualiza el `.section-num` y el menú.
- Los scripts de cada sección van inline al final de la sección (mapa en `#soa`, simulador en `#cotizador`). El script final maneja tema, menú, colapsables y búsqueda: un error ahí deja sin funcionar todo lo que sigue. **Usa `var` para variables que `setTheme()` o cualquier función del bloque inicial necesite leer; un `let` declarado después de su primer uso produce un TDZ ReferenceError silencioso que corta el resto del script.** (Este bug ya ocurrió con `panoramaChartsDrawn`.)
- El estado abierto/cerrado de secciones se persiste en `localStorage` bajo la clave `bolivia-open` (JSON array de IDs de sección, p. ej. `["panorama","cotizador"]`).
- **Datos embebidos**: las cifras están escritas a mano en arrays JS, no se leen del Excel en tiempo de ejecución:
  - `CUENTAS` (dentro de `#cuentas`): una entrada por cuenta del top 10 con `vol`, `pct`, `familias`, `planes`, `servicios`, `metodo`, `ruta`, `nota`. Las tarjetas y los filtros por familia se generan desde aquí.
  - `PROVEEDORES` (dentro de `#proveedores`).
  - `FAMILIAS_DATA` y `PLANES_DATA` (script final): gráficos de barras SVG del panorama (`svgBarChart`), redibujados al cambiar de tema.
  - `TARIFAS` y `czCalc` (dentro de `#cotizador`): réplica de las fórmulas del cuadro cotizador, con `console.assert` contra casos reales de la hoja. Si cambian tarifas o fórmulas, actualizar ambos y los asserts.
- Los KPIs y algunos textos repiten cifras en HTML. Si cambias un número, búscalo en todo el archivo.

## Datos

- Fuente de verdad: `transference_12-10-2026 11_38 a. m..xlsx`, hoja `Sheet1` (1.661 filas, una por asistencia; columnas clave: `Nombre_Cuenta`, `Nombre_Plan`, `Nombre_del_servicio`, `Familia_Servicio`, `Estado_de_Asistencia`, `Nombre_de_proveedor`, `Total_Monto_AA/CC/NA`).
- `Información Bolivia.xlsx`, hoja Dashboard: no es fiable (sus fórmulas cortan en la fila 1000). No la uses para cifras.
- `CAPACITACIÓN BOLIVIA 2026.pptx.txt`: protocolos y rutas de validación. Contiene errores conocidos (tipificación AA/CC/NA, "subcuenta"); las correcciones del usuario en `tasks/cambios.md` prevalecen sobre el pptx.
- Para recalcular cifras se usa Node con el paquete global `xlsx` (no hay Python):
  ```bash
  NODE_PATH="C:/Users/Edward Morales/AppData/Roaming/npm/node_modules" node script.js
  ```
  Escribe los scripts de análisis en el directorio temporal, no en el proyecto.
- `CUADRO COTIZADOR POR CUENTAS_2026.xlsx`: export de la hoja de Google Sheets que se usa para cotizar grúas. Al exportarla se pierde la protección de celdas; las celdas de entrada se reconocen por el color y las listas desplegables (`dataValidation` en el XML). Las pestañas NACIONAL 1 y 3 leen los precios de la tabla de NACIONAL 2. Contiene datos personales reales: no copiarlos al manual.
- Reglas de cálculo: excluir las cuentas **IKATECH** (prueba) y **Addiuva Enterprises** (interna); la base queda en 1.642 asistencias. En farmacia, "Cancelado posterior" es el cierre normal, no una cancelación.

## Convenciones de contenido

- Todo en español, texto directo y operativo, sin relleno de IA.
- "Cuenta", nunca "Sponsor". "Plan", nunca "subcuenta".
- Formato numérico es-BO en textos: `1.642`, `49,0 %`.
- No incluir credenciales de sistemas.
- Reglas operativas confirmadas (siniestros, 30 km y cuadro cotizador, TEA 15 min / 10 min BISA, DOKKA) están en `tasks/cambios.md`. Consúltalas antes de redactar protocolos.
