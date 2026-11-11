# Análisis de Mercado: AirB&B en la Ciudad de México (Otoño 2026)

## 📌 Descripción
Análisis del mercado de alquiler a corto plazo en CDMX utilizando datos abiertos de Inside Airbnb. El objetivo es identificar patrones de precio, ocupación y rentabilidad para saber dónde conviene invertir en la ciudad.

## 🧹 Proceso de Limpieza y Calidad de Datos
El dataset original (30,468 registros) presentaba varios retos de calidad que se resolvieron de la siguiente manera:
- Se redujo el número de columnas de 90 a 19.
- El archivo original presentaba problemas de codificación (UTF-8) que se resolvieron con `encoding_errors="replace"` y se hizo el cambio a latin-1.
- Ciertos valores como "$3,505.00", aparecían como texto, se limpiaron y convirtieron a tipo numérico (float).
- Se eliminaron 2,108 nulos en `price` y se imputaron 403 en `beds` usando la mediana por tipo de habitación. La columna `host_since` venía vacía, por lo que se usó `host_time_as_host_years` como un aproximado de la antigüedad del host.
- Se detectaron 37 registros con precios imposibles (>$50,000 MXN/noche) que se eliminaron por ser errores de captura. Los valores atípicos de lujo real se mantuvieron, pero se acotaron al percentil 99 (P99) para el análisis general.

**Dataset final:** 28,323 registros limpios y listos para el análisis.

## 🎯 Metodología y KPIs
Se calcularon métricas de negocio agrupadas por alcaldía, tipo de habitación y antigüedad del anfitrión, incluyendo:
- Precio mediano y promedio.
- Ocupación estimada anual (`estimated_occupancy_l365d`).
- Ingreso estimado anual (`price * estimated_occupancy_l365d`).

## ✨ Hallazgos Principales
1. La alcaldía Cuauhtémoc concentra el 46.6% de la oferta y el mayor ingreso estimado promedio ($204,760 MXN). Su oferta no tiene los precios más altos como la alcaldía Miguel Hidalgo, pero tiene la mejor combinación precio x ocupación.
2. Los anfitriones con 2-3 años de experiencia logran la ocupación más alta (101.89 días/año), mientras que los nuevos (0-1 año) solo alcanzan 68.89 días, tienen 33% menos ocupación que los intermedios.
3. Existe un nicho de ultra lujo de villas y mansiones en las colonias Condesa/Roma (hasta 9 recámaras) que, a pesar de cobrar entre $12,000 y $37,000 MXN por noche, mantienen ocupaciones de 150 a 255 días al año.
4. Rentar la casa o departamento completo genera 3.7 veces más ingresos que una habitación privada.
5. Las alcaldías Iztacalco, Cuajimalpa de Morelos y Venustiano Carranza son emergentes, ya que al no tener tanta presencia en esas zonas, en cuanto a ocupación le ganan o están a la par que las alcaldías con más turismo, es decir, Cuauhtémoc y Miguel Hidalgo. Y en cuanto a ingresos estimados, se posicionan por encima de alcaldías más populares como Coyoacán.
6. Las alcaldías Cuauhtémoc y Miguel Hidalgo, donde se encuentran las colonias muy famosas (Roma, Condesa y Polanco), se posicionan muy bien en cuanto a la relación precio-ocupación. A diferencia de las alcaldías Milpa Alta o Xochimilco, su ocupación es mucho menor ya que se encuentran muy lejos de donde está el núcleo turístico.

**Conclusión:** Conviene invertir en las alcaldías con atractivo turístico, ya que las personas están dispuestas a pagar el costo sin importar el precio.

## ⚠️ Limitantes
- No se incluyen costos operativos (limpieza, mantenimiento), por lo que el "ingreso estimado" no refleja el margen de ganancia real.
- La ocupación es una estimación de Inside Airbnb basada en calendarios, no una verdad absoluta.
- Algunos barrios tienen muy pocos registros (ej. Milpa Alta con 25), por lo que sus promedios no son estadísticamente representativos.

## 📊 Dashboard
<img width="1920" height="1043" alt="2026-11-11" src="https://github.com/user-attachments/assets/9c84cdbb-85ca-4a37-9fcf-c09788e5f81a" />

👉 [Haz clic aquí para ver el Dashboard interactivo en Tableau Public](https://public.tableau.com/views/AnlisisdeMercadoAirBBenlaCiudaddeMxicoOtoo2026/Dashboard1?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

## 💻 Código del Análisis
Puedes revisar el notebook completo con el proceso de limpieza, cálculo de KPIs y visualización de datos aquí:
👉 **[Ver Notebook de Jupyter (Análisis completo)](https://github.com/AleRR94/analisis-airbnb-cdmx/blob/main/notebook/limpieza_airbnb_cdmx.ipynb)**


### 🧾 Fuente de datos
https://insideairbnb.com/get-the-data/ Consultado el 20 de octubre de 2026
