# Análisis de Mercado: Airbnb en la Ciudad de México (Otoño 2026)

## 📌 Descripción
Análisis del mercado de alquiler a corto plazo en CDMX utilizando datos abiertos de Inside Airbnb. El objetivo es identificar patrones de precio, ocupación y rentabilidad para entender dónde conviene invertir en la ciudad.

## 🧹 Calidad y Limpieza de Datos
El dataset original (30,468 registros) presentaba los siguientes retos de calidad:
1. **Encoding mixto:** Se resolvió con `encoding_errors="replace"`.
2. **Precios como texto:** Valores como "$3,505.00" requerían limpieza y casteo a float.
3. **Datos faltantes:** 2,108 nulos en `price` (eliminados) y 403 en `beds` (imputados con mediana por tipo de habitación).
4. **Outliers extremos:** Se detectaron 37 registros con precios imposibles (>$50,000 MXN/noche) que fueron eliminados por ser errores de captura. El resto de valores atípicos (lujo real) se mantuvieron, pero se acotaron al P99 para el análisis general.

**Dataset final:** 28,323 registros limpios y listos para análisis.

## 🎯 Metodología y KPIs
Se calcularon métricas de negocio agrupadas por barrio, tipo de habitación y antigüedad del host, incluyendo:
- Precio mediano y promedio.
- Ocupación estimada anual (`estimated_occupancy_l365d`).
- Ingreso estimado anual (`price * estimated_occupancy_l365d`).

## ✨ Hallazgos Principales
1. **Cuauhtémoc domina el mercado:** Concentra el 46.6% de la oferta y el mayor ingreso estimado promedio ($204,760 MXN).
2. **El precio no lo es todo:** Los anfitriones con 2-3 años de experiencia logran la ocupación más alta (101.89 días/año), mientras que los nuevos (0-1 año) solo alcanzan 68.89 días.
3. **El mercado de ultra-lujo:** Existe un nicho de villas y mansiones en Condesa/Roma (hasta 9 recámaras) que, a pesar de cobrar entre $12,000 y $37,000 MXN por noche, mantienen ocupaciones de 150 a 255 días al año.
4. **Entire home/apt** genera 3.7 veces más ingresos que una habitación privada.

## ⚠️ Limitantes
- No se incluyen costos operativos (limpieza, mantenimiento), por lo que el "ingreso estimado" no refleja el margen de ganancia real.
- La ocupación es una estimación de Inside Airbnb basada en calendarios, no una verdad absoluta.
- Algunos barrios tienen muy pocos registros (ej. Milpa Alta con 25), por lo que sus promedios no son estadísticamente representativos.

## 📊 Dashboard
👉 [Haz clic aquí para ver el Dashboard interactivo en Tableau Public](ENLACE_AQUI)
