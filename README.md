# 📊 V3 DashboardBI — Reporte de Ventas en Power BI

V3 DashboardBI es un reporte de ventas en Power BI con esquema estrella (6 dimensiones). Incluye páginas de Overview y Detalle de Ventas con KPIs, gráficos interactivos, mapa, tooltip personalizado, formato condicional y diseño mobile. Período de datos: 2023–2024.

---

## 📸 Capturas

### Overview
![Overview](overview.png)

### Detalle de Ventas
![Detalle de Ventas](detalle.png)

### Vista Mobile — Overview
![Mobile Overview](mobile_overview.png)

### Vista Mobile — Detalle de Ventas
![Mobile Detalle](mobile_detalle.png)

---

## 📁 Estructura del Proyecto

```
📦 V3 DashboardBI
 ┣ 📄 V3 DashboardBI.pbix       # Archivo principal del reporte
 ┗ 📄 Documentacion_V3_DashboardBI.docx  # Documentación técnica completa
```

---

## 🗂️ Modelo de Datos

Esquema estrella con **1 tabla de hechos** y **6 dimensiones**:

| Tabla | Tipo | Descripción |
|---|---|---|
| `Ventas` | Hechos | Transacciones de venta con métricas y claves foráneas |
| `Clientes` | Dimensión | Segmento, ciudad, datos del cliente |
| `Producto` | Dimensión | Categoría, subcategoría, tamaño, precios |
| `Territorio` | Dimensión | Ciudad, zona, provincia, latitud y longitud |
| `Vendedor` | Dimensión | Región, sucursal, meta de ventas |
| `Medios_de_Pago` | Dimensión | Tipo, moneda, recargo |
| `Calendario` | Dimensión | Año, mes, trimestre, ordenamiento cronológico |

> **Relación de fecha activa:** `Ventas[Fecha_Entrega] → Calendario[Date]`

---

## 📐 Medidas DAX

| Medida | Expresión |
|---|---|
| Ventas Totales | `SUM(Ventas[Precio_Venta_Final])` |
| Costos Totales | `SUM(Ventas[Costo_Total])` |
| Rentabilidad | `SUM(Ventas[Rentabilidad])` |
| Unidades Vendidas | `SUM(Ventas[Cantidad])` |
| Promedio Diferencia Dias | `AVERAGE(Ventas[Diferencia_Dias])` |
| Fecha Actual | `"Hoy: " & FORMAT(TODAY(), "DD/MM/YYYY")` |
| Ultima Actualizacion | `"Últ. actualización: " & FORMAT(MAX(Ventas[Fecha_Entrega]), "DD/MM/YYYY")` |
| Color Promedio Dias | `IF([Promedio Diferencia Dias] < 15, "#00B050", "#FF0000")` |

---

## 📄 Páginas del Reporte

### 1. Overview
Visión general del negocio para toma de decisiones rápida.

- 4 KPIs: Ventas Totales, Costos Totales, Rentabilidad, Unidades Vendidas
- Gráfico evolutivo de ventas y rentabilidad por Mes-Año (con **tooltip personalizado**)
- Gráfico de líneas: ventas y rentabilidad por medio de pago
- Gráfico de barras: costo promedio por tamaño de producto
- Navbar de navegación entre páginas
- Indicadores dinámicos de fecha actual y última actualización

### 2. Detalle de Ventas
Página analítica con filtros interactivos.

- 3 segmentadores: fecha (rango), ciudad (dropdown), medio de pago (dropdown)
- 4 KPIs incluyendo Promedio Diferencia Días con **formato condicional** (verde < 15 días / rojo ≥ 15 días)
- Gráfico de líneas: evolución de ventas por mes
- Gráfico de barras: ventas por zona
- Gráfico de barras agrupadas: ventas por medio de pago y segmento de cliente
- Matriz: unidades vendidas por categoría y rango de tiempo de entrega
- Mapa con burbujas por latitud/longitud y tamaño proporcional a ventas

### 3. Tooltip Overview *(página auxiliar)*
Mini panel que aparece al hacer hover sobre el gráfico evolutivo de Overview:
- Tarjeta de Ventas Totales
- Tarjeta de Costos Totales
- Gráfico de Rentabilidad por Zona

---

## 📱 Diseño Mobile

Ambas páginas tienen layout mobile optimizado para dispositivos móviles, con visuales reorganizados verticalmente y KPIs en grilla 2×2.

---

## ⚙️ Columnas Calculadas

| Columna | Tabla | Descripción |
|---|---|---|
| `Rango Diferencia Dias` | Ventas | Agrupa días en: Rápido / Normal / Demorado / Muy demorado |
| `Orden Rango Dias` | Ventas | Orden numérico (1–4) para sortear el rango cronológicamente |

---

## 🛠️ Requisitos

- Power BI Desktop (versión compatible con nivel de compatibilidad 1600+)
- Conexión a fuente de datos original para actualizar

---

## 📝 Documentación

La documentación técnica completa está disponible en el archivo `Documentacion_Dashboard.docx`, que incluye descripción del modelo, medidas DAX, detalle de páginas y notas técnicas.
