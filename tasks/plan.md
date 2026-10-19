# Plan: Documento de Capacitación Operativa Bolivia — Addiuva

## Objetivo
Producir un único archivo `capacitacion-bolivia.html` autocontenido (sin dependencias externas en runtime) que funcione como:
- **Referencia diaria** para coordinadores y cabinas
- **Material de presentación** para capacitaciones

> Las reglas confirmadas por el usuario y el detalle de cada cambio están en `tasks/cambios.md`. Si este plan y cambios.md no coinciden, vale cambios.md.

## Fuentes de datos confirmadas
| Fuente | Qué aporta |
|---|---|
| `transference_12-10-2026.xlsx` | 1.661 asistencias en bruto (1-ago a 12-oct-2026). El manual usa **1.642**: se excluyen IKATECH (prueba) y Addiuva Enterprises (interna). Volúmenes, cuentas, planes, servicios, proveedores, estados, tipificación AA/CC/NA |
| `CAPACITACIÓN BOLIVIA 2026.pptx.txt` | Protocolos operativos, rutas de validación por cuenta, TEA, sistemas, tipificación financiera, farmacias, reembolsos, terminología local. Tiene errores conocidos (AA/CC/NA, "subcuenta", foto de fachada): prevalecen las correcciones del usuario |
| `dashboard.html` | Visualizaciones anteriores. Sus cifras usan la base de 1.661 y no se actualizan |
| `Información Bolivia.xlsx` | No usar la hoja Dashboard: sus fórmulas cortan en la fila 1000 |

## Grafo de dependencias

```
[T1: Scaffold HTML]
       │
       ├── [T2: Panorama Bolivia]       ← Excel data
       ├── [T3: SOA + Datos obligatorios] ← Slides
       ├── [T4: Top 10 Cuentas]         ← Excel + Slides
       ├── [T5: Proveedores]            ← Excel + Slides
       ├── [T5b: Servicios No Viales]   ← Slides + reglas del usuario (añadida el 14-oct-2026)
       ├── [T6: Plataformas y sistemas] ← Slides
       ├── [T7: Tipificación AA/CC/NA]  ← Slides
       ├── [T8: Reembolsos y Farmacias] ← Slides
       └── [T9: Errores + Terminología] ← Slides
              │ (todos)
       [T10: Polish: PDF, nav, búsqueda]
```

T1 primero. T2–T9 independientes entre sí, paralelos en ejecución. T10 cierra.

---

## Tareas

### T1 — Scaffold HTML base
**Descripción:** Crear `capacitacion-bolivia.html` con estructura completa: barra lateral de navegación con todas las secciones, header con logo/título, sistema de temas (dark por defecto), estilos CSS inlineados, Chart.js inlineado (sin CDN), esqueletos de sección vacíos con IDs.

**Criterios de aceptación:**
- Abre en browser sin conexión a internet
- Navegación lateral lleva a cada sección sin recarga
- Sección activa se marca visualmente en el nav
- Chart.js disponible globalmente (inline o bundle mínimo)
- Responsive: legible en pantalla 1280px y en A4 impreso

**Verificación:** Abrir en Chrome offline → nav funciona → F12 sin errores de red → Ctrl+P muestra estructura limpia

---

### T2 — Sección: Panorama de la Operación
**Descripción:** Resumen ejecutivo de la operación Bolivia con datos reales del Excel.

**Contenido:**
- 6 KPIs: total asistencias, concluidas, canceladas, en proceso, cuentas activas, proveedores
- Gráfico donut: distribución por familia de servicio (Vehicular 761, Médica 658, Hogar 101, Mascota 70, Telemedicina 34, otros 18)
- Gráfico donut: estados de asistencias (Concluida 804, Cancelado posterior 486, Cancelado al momento 240, En proceso 112)
- Contexto Bolivia: 9 departamentos, prefijos de área como ancla geográfica
- Nota editorial: la cancelación bruta es del 44,2 %, pero 382 de esas cancelaciones son cierres normales de farmacia. Sin farmacia, la cancelación es del 27,3 % (344 de 1.259)

**Criterios de aceptación:**
- KPIs visibles sin scroll en 1280px
- Ambos gráficos renderizan sin CDN
- Los números coinciden exactamente con el Excel procesado

**Verificación:** Comparar números contra output del script Node ya ejecutado

---

### T3 — Sección: Sistema SOA y Datos Obligatorios
**Descripción:** Guía visual del flujo de validación obligatorio antes de coordinar cualquier servicio.

**Contenido:**
- Checklist de 5 datos obligatorios (Nombre, CI, Teléfono, Placa/Dirección, Prefijo departamental)
- Mapa interactivo con límites reales, coloreado por región (occidente, valles, oriente), y tabla de departamentos con capital, ciudades, región y código de área. Jerga regional boliviana
- Diagrama Cuenta → Plan → Servicio (por qué no asumir cobertura solo por la cuenta)
- ~~Semáforo de estados SOA: ACTIVO (verde), INACTIVO (rojo), BLOQUEADO (amarillo) con acción por estado~~ — **descartado por el usuario (13-oct-2026)**
- Regla de oro: nunca avanzar sin validar el plan específico

**Criterios de aceptación:**
- ~~Semáforo con 3 colores y acción clara por estado~~ (descartado)
- Checklist interactivo (marcar/desmarcar, estado no persiste al recargar — OK)
- Diagrama entendible en 5 segundos

**Verificación:** Mostrar a alguien nuevo → puede nombrar los 5 datos obligatorios y el prefijo de su departamento

---

### T4 — Sección: Top 10 Cuentas
**Descripción:** Cards individuales por cada cuenta con datos operativos completos.

**Contenido por card:**
- Nombre, volumen total, % del total de asistencias
- Top 5 servicios utilizados (datos del Excel) con barra visual
- Ruta de validación específica (datos de slides: Alianza=portal web CI, Nacional Vial=App, Nacional Vagoneta=SOA+correo, Bisa=WhatsApp, Bancos=SOA)
- Nota crítica de gestión (ej. "Nacional: cruzar plan Vial vs Vagoneta SIEMPRE")
- Familia de servicio predominante (badge de color: Vehicular/Médica/Hogar/Mascota/Mixta)
- Subtítulo con los planes de la cuenta y su volumen (hasta 3 y "+N más")
- Reglas específicas por cuenta (pptx, diap. 08)

**Cuentas a cubrir (% sobre 1.642):**
1. Nacional Seguros Patr. y Fianzas (769) — Vehicular dominante
2. Asist. Nacional Seguros Vida y Salud (253) — Médica/Farmacia
3. Alianza Seguros (183) — Consultas médicas presenciales
4. La Boliviana Ciacruz (131) — Descuento medicamentos
5. Asistencia Banco FIE (81) — Farmacia
6. Asistencia Banco Ecofuturo (62) — Farmacia
7. Banco Económico (58) — Hogar/Mascota mixto
8. BISA Seguros (50) — Vehicular + Farmacia, TEA 10 min
9. Credinform International (15) — Traslado ocupantes
10. Banco Fortaleza (13) — Farmacia (reemplaza a IKATECH, que se excluye por ser cuenta de prueba)

**Criterios de aceptación:**
- 10 cards renderizadas, filtrables por familia (botones: Todas, Vehicular, Médica, Hogar, Mascota, con conteo). Cada cuenta aparece en cada familia donde tiene 5 o más asistencias
- Cada card tiene ruta de validación claramente diferenciada
- Números exactos del Excel

**Verificación:** Filtrar por "Hogar" → aparecen Nacional, Banco Económico, La Boliviana y Asist. Nacional Vida y Salud

---

### T5 — Sección: Proveedores Clave
**Descripción:** Directorio operativo de proveedores con métricas reales.

**Contenido:**
- Tabla top 15 proveedores con volumen, tipo (Grúas/Farmacia/Médico/Otro)
- Card destacada Full Assistance: protocolo WhatsApp, tarifas (Bs. 230 <10km, Bs. 300 <30km, Bs. 16/km extra, Bs. 150 maniobra especial), radio máx 30km
- Grupo farmacias: Farmacorp (70), Farmacia Económica (47), Farmacias Chávez (42) — reglas de receta
- Grupo grúas: Full Assistance, Full Auto, Grúas Mérida (Cbba+SCZ), Auto Rueda, Arce Motors, Grúas Salvatierra
- Nota: Cotizador Drive obligatorio para provincias

**Criterios de aceptación:**
- Tarifas Full Assistance en tabla con highlight visual (no escondidas en texto)
- Proveedores agrupados por categoría
- Top 15 ordenados por volumen con número visible

**Verificación:** Alguien puede responder "¿cuánto cuesta remolque a 25km?" solo mirando la sección

---

### T6 — Sección: Plataformas y Sistemas
**Descripción:** Guía de cuándo y cómo usar cada sistema.

**Sistemas a cubrir:**
| Sistema | Para qué | Cuándo |
|---|---|---|
| SOA | Validación, expedientes, tipificación | Siempre primero |
| CallBell | WhatsApp afiliados y proveedores | Canal único escrito |
| Vicidial | Tipificación final de llamada | Al cerrar llamada |
| DOKKA | Ticketera de Nacional: recibir solicitudes viales y derivar o escalar casos (incluidos siniestros) | Solo Nacional. Las solicitudes viales por DOKKA son exclusivas de Nacional (confirmado el 15-oct-2026) |
| App Mi Seguro | Validar Nacional Plan Vial | Solo cuenta Nacional Vial |
| Portal Alianza | Validar Alianza por CI | Solo cuenta Alianza |
| Cotizador Drive | Calcular km/costo en provincia | Servicio fuera de capital |

**Contenido extra:** Flujo de cierre operativo (SOA → CallBell → Vicidial) y reglas de oro DOKKA

**Criterios de aceptación:**
- Tabla con columnas: Sistema / Propósito / Cuándo usarlo / Nota clave
- Flujo de cierre como diagrama de pasos numerados
- 3 reglas de oro DOKKA visualmente destacadas

**Verificación:** ¿Cuándo uso DOKKA vs cuándo uso SOA? Respondible en <10 segundos

---

### T7 — Sección: Tipificación Financiera AA / CC / NA
**Descripción:** La sección más crítica para evitar errores de auditoría.

**Definiciones (validadas por el usuario el 13-oct-2026 — el pptx, diapositiva 12, está mal y no debe usarse como fuente):**
| Código | Quién paga | Cuándo |
|---|---|---|
| **AA** | Addiuva | Servicio dentro de cobertura, o costo que Addiuva asume por un error propio |
| **CC** | La cuenta | Solicitud fuera de cobertura que la cuenta asume como excepción, sin trasladarla al afiliado |
| **NA** | El afiliado | Excedente o servicio en conexión no cubierto por su póliza |

**Contenido:**
- 3 cards con colores distintos: AA (azul), CC (verde), NA (dorado)
- Definición de cada código
- Árbol de decisión en orden: 1) ¿dentro del plan? → AA · 2) ¿error de la cabina? → AA + escalar · 3) ¿la cuenta autorizó la excepción? → CC · 4) resto → NA
- Ejemplos concretos: remolque en cobertura = AA, km excedente = NA (o CC si la cuenta lo autoriza)
- Alerta de error frecuente: tipificar todo como AA cuando hay excedente

**Criterios de aceptación:**
- Árbol de decisión interactivo o visual (no texto plano)
- Los 3 códigos visibles en una sola pantalla sin scroll
- Al menos 2 ejemplos por código

**Verificación:** Caso práctico: "remolque con 5km de excedente" → operador identifica AA + NA sin dudar

---

### T8 — Sección: Reembolsos y Módulo Farmacias
**Descripción:** Dos flujos distintos pero relacionados.

**Reembolsos:**
- Requisitos de factura (Razón Social, NIT de la cuenta, concepto detallado)
- 16% retención DS 4850 para particulares
- Plazo: 3–7 días hábiles post-aprobación
- Error crítico: NIT incorrecto = rechazo contable

**Farmacias:**
- Flujo: validar en SOA → receta física (firma + fecha + saldos) → confirmar límite mensual → coordinar con farmacia
- Cuentas que usan descuento farmacia: 10 cuentas y 383 asistencias (tabla completa en el HTML, sección 08). Las principales: La Boliviana (116), Asist. Nal. V&S (85), FIE (78), Ecofuturo (62)
- Si el registro falla: escalar al supervisor indicando la antigüedad del afiliado
- Regla: sin validación SOA o receta válida → no se coordina

**Criterios de aceptación:**
- Flujo de farmacia como pasos numerados (no bullet points)
- Alerta visual para el tema del NIT
- Tabla de cuentas con descuento farmacia y volumen

**Verificación:** El flujo de farmacia tiene exactamente los pasos en orden correcto del manual

---

### T9 — Sección: Errores Frecuentes y Terminología Local
**Descripción:** Referencia rápida para evitar los desvíos más comunes.

**Errores frecuentes (de slides):**
- Omitir validación CI inicial
- Confundir códigos financieros AA/CC/NA
- No calcular km exactos para provincias (no usar Cotizador)
- Gestionar siniestros en cabina (debe ir a DOKKA)
- Asumir cobertura por la cuenta sin verificar el plan

**Terminología boliviana:**
- "Surtidor" = gasolinera/estación de servicio
- "Trancadera" = atasco/embotellamiento de tráfico
- "Carnet" = documento de identidad nacional
- Prefijos departamentales (mapa de códigos de área)
- Modismos de trato: "don/doña", formalidad esperada

**Criterios de aceptación:**
- Errores en formato tabla: Situación / Error frecuente / Acción correcta
- Glosario con al menos 8 términos
- Sección visualmente diferenciada (fondo distinto o borde de alerta)

**Verificación:** Un nuevo coordinador puede identificar los 5 errores críticos en menos de 2 minutos

---

### T10 — Polish: navegación, PDF, búsqueda
**Descripción:** Capa final de usabilidad.

**Acciones:**
- CSS `@media print` para output A4 limpio (ocultar nav lateral, expandir contenido)
- Indicador de progreso de scroll
- Búsqueda rápida por texto (input que filtra secciones visibles)
- Tabla de contenidos con anclas y tiempos estimados de lectura por sección
- Pie de página con fecha de última actualización y fuente del dato

**Criterios de aceptación:**
- Ctrl+P produce PDF legible con todas las secciones
- Búsqueda filtra en tiempo real
- Sin errores en consola del browser

**Verificación:** Imprimir en PDF → revisar cada sección renderiza correctamente

---

## Checkpoints de revisión humana

| CP | Después de | Pregunta al usuario |
|---|---|---|
| **CP1** | T1 (scaffold) | ¿El diseño, estructura de nav y paleta de colores son los correctos antes de llenar contenido? |
| **CP2** | T2 + T3 + T4 | ¿Los datos de cuentas y el panorama reflejan la realidad de la operación? ¿Falta alguna cuenta o dato? |
| **CP3** | T5 + T6 + T7 | ¿Los protocolos de proveedores, sistemas y tipificación son precisos? |
| **CP4** | T8 + T9 | ¿Los flujos de farmacia y reembolsos están completos? ¿El glosario cubre términos importantes? |
| **CP5** | T10 (final) | Revisión final: abrir, navegar, imprimir. Go / No-go. |

---

## Decisiones de diseño
- **Sin CDN en runtime**: Chart.js 4.4.0 va embebido en el HTML (hecho el 13-oct-2026). Si no carga, los gráficos se muestran como lista
- **Colores por significado**: tokens CSS `--fam-*` para familias de servicio (Vehicular azul, Médica verde, Hogar naranja, Mascota violeta, Mixta gris) y `--st-*` para estados (verde concluida, rojo cancelada, ámbar en proceso). Gráficos y badges leen los mismos tokens. Rojo/ámbar/verde no se usan para familias
- **Accesibilidad mínima**: contraste WCAG AA en textos, `h1`/`h2` reales, foco visible, navegable con teclado
- **Móvil**: bajo 900px la barra lateral se abre con el botón ☰
- **Un solo archivo HTML**: sin imágenes externas, sin JS externo, sin CSS externo
- **Tema**: sigue la preferencia del sistema (`prefers-color-scheme`) y recuerda la elección del usuario (`localStorage`)
- **Credenciales**: no se incluyen credenciales de sistemas en el manual (decisión del usuario)
- **Terminología**: "Cuenta" (nunca "Sponsor") y "plan" (nunca "subcuenta")
- **Secciones**: 01 Panorama · 02 SOA · 03 Cuentas · 04 Proveedores · 05 Servicios No Viales · 06 Plataformas · 07 Tipificación · 08 Cuadro Cotizador · 09 Reembolsos y Farmacias · 10 Errores y Terminología
