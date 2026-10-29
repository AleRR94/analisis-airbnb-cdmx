# Análisis de Mercado: AirB&B en la Ciudad de México (Otoño 2026)

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
1. Reduje el número de columna de 90 a 19.
2. El archivo original tenía caracteres con un sistema viejo (UTF-8) por lo tanto no los reconocía, se hizo el cambio a latin-1.
3. La columna "host_since" viene vacía, por lo que usé "host_time_as_host_years" como aproximado de la antigüedad del anfitrión.
4. Se eliminaron outliers de precios exagerados por habitación, debido a que una habitación privada jamás costaría eso.
5. Se calcularon métricas de negocio agrupadas por barrio, tipo de habitación y antigüedad del host, incluyendo:
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
7. En conclusión, conviene invertir en las alcaldías con el polo de atracción turística, ya que las personas quieren hospedarse ahí sin importar el costo.

## ⚠️ Limitantes
- No se incluyen costos operativos (limpieza, mantenimiento), por lo que el "ingreso estimado" no refleja el margen de ganancia real.
- La ocupación es una estimación de Inside Airbnb basada en calendarios, no una verdad absoluta.
- Algunos barrios tienen muy pocos registros (ej. Milpa Alta con 25), por lo que sus promedios no son estadísticamente representativos.

## 📊 Dashboard
👉 [Haz clic aquí para ver el Dashboard interactivo en Tableau Public](https://public.tableau.com/views/AnlisisdeMercadoAirBBenlaCiudaddeMxicoOtoo2026/Dashboard1?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
