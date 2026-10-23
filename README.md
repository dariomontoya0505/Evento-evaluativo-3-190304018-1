# Análisis de Datos Airbnb Bogotá – Evento Evaluativo 3

## Business Intelligence, análisis estadístico y visualización de datos

**Institución:** Institución Universitaria ITM  
**Programa:** Ingeniería de Sistemas  
**Curso:** Análisis de Datos  
**Semestre:** 2026-2  
**Proyecto asignado:** Equipo 10 – Airbnb  

---
## 1. Descripción del proyecto

Este proyecto desarrolla un análisis de Business Intelligence sobre la oferta de alojamientos de Airbnb en Bogotá, utilizando datos de **Inside Airbnb** correspondientes a una captura del **16 de septiembre de 2026**.

El propósito es transformar los datos disponibles en información útil para apoyar la comprensión del mercado de alojamientos, mediante preparación y modelado de datos, indicadores clave de desempeño (KPIs), pruebas estadísticas, visualizaciones y un dashboard ejecutivo desarrollado en Tableau.

El proyecto analiza principalmente la relación del precio con la localidad, el tipo de alojamiento, la capacidad del inmueble y la calificación. También compara el comportamiento de anfitriones con un solo anuncio frente a anfitriones con varios anuncios.

El archivo fuente contiene **19.505 anuncios**. Después del proceso de preparación y aplicación de los criterios definidos para el análisis, se obtiene una población analítica de **17.998 anuncios**.

---

## 2. Problema de análisis

La oferta de Airbnb en Bogotá presenta diferencias entre alojamientos en aspectos como precio, ubicación, capacidad, tipo de alojamiento, calificación, actividad reciente y características del anfitrión.

Observar estas variables de manera aislada no permite establecer si las diferencias identificadas son suficientemente consistentes desde el punto de vista estadístico ni cuáles factores presentan una asociación más clara con el precio.

Por esta razón, el proyecto busca responder, mediante evidencia descriptiva y estadística, **qué características permiten explicar las principales diferencias observadas en la oferta de Airbnb en Bogotá y cómo pueden resumirse mediante indicadores y visualizaciones útiles para la toma de decisiones**.

---

## 3. Objetivo general

Analizar los datos de alojamientos Airbnb en Bogotá mediante técnicas de Business Intelligence y análisis estadístico, con el fin de identificar patrones, diferencias y relaciones entre el precio y variables relevantes del alojamiento y del anfitrión, presentando los resultados mediante KPIs, pruebas de hipótesis y dashboards interactivos.

### Objetivos específicos

1. Preparar, limpiar y transformar el dataset original para construir una base analítica consistente.
2. Estructurar los datos mediante dimensiones, métricas y tablas orientadas al análisis.
3. Definir indicadores clave que permitan resumir el comportamiento general de la oferta.
4. Evaluar estadísticamente diferencias de precio según localidad y tipo de alojamiento.
5. Analizar la relación entre capacidad, calificación y precio.
6. Comparar indicadores entre anfitriones con un solo anuncio y anfitriones con varios anuncios.
7. Construir visualizaciones y dashboards en Tableau para comunicar los principales resultados.
8. Formular conclusiones, limitaciones y posibles decisiones basadas en la evidencia obtenida.

---

## 4. Preguntas de análisis

El proyecto se orienta a responder las siguientes preguntas:

1. **¿Existen diferencias estadísticamente significativas en el precio de los alojamientos entre las localidades de Bogotá?**
2. **¿El tipo de alojamiento está asociado con diferencias en los precios publicados?**
3. **¿Existe relación entre la capacidad de alojamiento y su precio?**
4. **¿Existe relación entre la calificación del alojamiento y su precio?**
5. **¿Los anfitriones con varios anuncios presentan un comportamiento diferente frente a los anfitriones con un solo anuncio en variables de precio, ocupación, reseñas y calificación?**

---

## 5. Fuente de datos

- **Fuente:** Inside Airbnb
- **Archivo utilizado:** `datos/listings_bogota.csv`
- **Fecha de captura registrada en el dataset:** 2026-09-16
- **Registros originales:** 19.505
- **Columnas originales:** 90
- **Columnas completamente vacías identificadas:** 14
- **Columnas conservadas durante la preparación:** 35

El proyecto conserva información de trazabilidad del archivo fuente mediante SHA-256 dentro de los archivos de control generados por la fase de preparación.

---

## 6. Metodología

El proyecto se desarrolló por fases, siguiendo el proceso establecido para el Evento Evaluativo 3.

### Fase 1 – Comprensión del problema

Se definió el contexto del análisis de Airbnb Bogotá, el problema analítico y las preguntas que orientan el estudio.

### Fase 2 – Formulación de hipótesis

Se formularon cinco hipótesis relacionadas con:

- precio y localidad;
- precio y tipo de alojamiento;
- capacidad y precio;
- calificación y precio;
- características de anfitriones con uno o varios anuncios.

### Fase 3 – Preparación y modelado de datos

La preparación se realiza en:

`01_preparacion_datos.ipynb`

El proceso incluye:

- carga del archivo fuente;
- selección de variables;
- análisis de calidad;
- tratamiento del precio;
- identificación de valores atípicos;
- transformación de atributos;
- construcción de métricas derivadas;
- estructuración de dimensiones;
- construcción de tabla de hechos;
- generación de tablas analíticas;
- registro de exclusiones;
- creación del diccionario de datos;
- exportación de archivos de control.

Para el precio se utiliza el formato original de la fuente y los valores atípicos se identifican aplicando el criterio de **1,5 × rango intercuartílico (RIQ) sobre el logaritmo del precio**.

No se imputa la calificación cuando esta se encuentra ausente.

Después de la preparación:

- Registros originales: **19.505**
- Anuncios incluidos en el análisis: **17.998**
- Anfitriones analizados: **7.795**
- Anfitriones con un anuncio: **5.417**
- Anfitriones con dos o más anuncios: **2.378**
- Calificaciones válidas dentro de la población analítica: **14.549**
- Calificaciones faltantes dentro de la población analítica: **3.449**

### Modelo de datos generado

La fase de preparación crea, entre otros, los siguientes archivos:

- `fact_anuncios.csv`
- `dim_localidad.csv`
- `dim_tipo_alojamiento.csv`
- `dim_anfitrion.csv`
- `airbnb_bogota_analitico.csv`
- `anfitriones_resumen.csv`
- `muestra_h1_localidad.csv`
- `muestra_h2_tipo_alojamiento.csv`
- `anuncios_excluidos.csv`
- `calidad_variables.csv`
- `registro_limpieza.csv`
- `diccionario_datos.csv`
- `informe_preparacion.json`

---

## 7. Hipótesis

Se trabajó con un nivel de significancia de **α = 0,05**.

### H1 – Precio según localidad

**H0:** La distribución del precio es igual entre las localidades incluidas en el análisis.

**H1:** Al menos una localidad presenta una distribución de precios diferente.

**Prueba:** Kruskal-Wallis.  
**Análisis complementario:** prueba post-hoc de Dunn con ajuste de Holm.

### H2 – Precio según tipo de alojamiento

**H0:** La distribución del precio es igual entre los diferentes tipos de alojamiento.

**H1:** Al menos un tipo de alojamiento presenta una distribución de precios diferente.

**Prueba:** Kruskal-Wallis.  
**Análisis complementario:** Dunn con ajuste de Holm y comparación bilateral Mann-Whitney entre vivienda completa y habitación privada.

### H3 – Capacidad y precio

**H0:** No existe asociación monotónica entre la capacidad del alojamiento y el precio.

**H1:** Existe asociación monotónica entre la capacidad del alojamiento y el precio.

**Prueba:** correlación de Spearman.

### H4 – Calificación y precio

**H0:** No existe asociación monotónica entre la calificación del alojamiento y el precio.

**H1:** Existe asociación monotónica entre la calificación del alojamiento y el precio.

**Prueba:** correlación de Spearman.

### H5 – Tipo de anfitrión

Para esta hipótesis se compara a los anfitriones que tienen un solo anuncio con aquellos que tienen dos o más anuncios.

**H0:** No existen diferencias entre ambos grupos de anfitriones en los indicadores evaluados.

**H1:** Existen diferencias entre ambos grupos de anfitriones en al menos uno de los indicadores evaluados.

Los indicadores evaluados son:

- precio mediano;
- ocupación media estimada;
- promedio de reseñas en los últimos 12 meses;
- calificación mediana.

**Prueba:** Mann-Whitney bilateral.  
**Corrección por comparaciones múltiples:** Holm sobre los cuatro indicadores.

---

## 8. KPIs

Los KPIs se calculan en:

`02_kpis_dashboard.ipynb`

El proyecto define seis indicadores.

| ID | Indicador | Resultado |
|---|---|---:|
| K1 | Precio mediano por noche | **160.000 COP** |
| K2 | Precio mediano por huésped | **60.000 COP** |
| K3 | Calificación promedio | **4,704 / 5** |
| K4 | Anuncios con reseñas en los últimos 12 meses | **67,18 %** |
| K5 | Ocupación estimada mediana | **6,58 %** |
| K6 | Anfitriones con varios anuncios | **30,51 %** |

### Interpretación de los KPIs

**K1 – Precio mediano por noche**

La mediana del precio de los 17.998 anuncios analizados es de **160.000 COP**. Se utiliza la mediana porque el precio presenta una distribución que puede verse afectada por valores extremos y asimetría.

**K2 – Precio mediano por huésped**

El precio mediano normalizado por capacidad es de **60.000 COP por huésped**. Este indicador permite comparar alojamientos considerando el número de personas que pueden hospedar.

**K3 – Calificación promedio**

Entre los **14.549 anuncios con calificación válida**, la calificación promedio es aproximadamente **4,704 sobre 5**.

**K4 – Actividad reciente**

El **67,18 %** de los anuncios analizados presenta al menos una reseña durante los últimos 12 meses. Este indicador sirve como aproximación a la actividad reciente de los alojamientos.

**K5 – Ocupación estimada**

La mediana de la variable de ocupación estimada calculada en el proyecto es de **6,58 %**. Debe interpretarse como una estimación derivada de la metodología del análisis y no como una medición directa de reservas reales de Airbnb.

**K6 – Anfitriones con varios anuncios**

De los **7.795 anfitriones** incluidos en el resumen analítico, **2.378** tienen dos o más anuncios. Esto corresponde al **30,51 %** de los anfitriones analizados.

---

## 9. Resultados estadísticos

Las pruebas se ejecutan en:

`03_contrastes_hipotesis.ipynb`

### H1 – Precio por localidad

- Prueba: Kruskal-Wallis
- n = **17.945**
- Estadístico H = **2304,06**
- p < **0,001**
- Tamaño de efecto η²H = **0,128**
- Decisión: **rechazar H0**

**Interpretación:** existen diferencias estadísticamente significativas en las distribuciones de precio entre las localidades incluidas en el contraste.

El análisis post-hoc de Dunn con corrección de Holm permite identificar específicamente entre cuáles localidades se presentan diferencias.

### H2 – Precio por tipo de alojamiento

- Prueba: Kruskal-Wallis
- n = **17.971**
- Estadístico H = **4159,82**
- p < **0,001**
- Tamaño de efecto η²H = **0,231**
- Decisión: **rechazar H0**

**Interpretación:** existen diferencias estadísticamente significativas en los precios según el tipo de alojamiento.

Como comparación prevista adicional, se evaluó vivienda completa frente a habitación privada:

- Prueba: Mann-Whitney bilateral
- n = **17.894**
- p < **0,001**
- Delta de Cliff = **0,623**
- Decisión: **rechazar H0**

Este resultado evidencia una diferencia clara entre ambos tipos de alojamiento dentro de la muestra evaluada.

### H3 – Capacidad y precio

- Prueba: correlación de Spearman
- n = **17.998**
- ρ = **0,480**
- p < **0,001**
- Decisión: **rechazar H0**

**Interpretación:** se identifica una asociación positiva entre la capacidad del alojamiento y el precio. Dentro de los datos analizados, los alojamientos con mayor capacidad tienden a presentar precios más altos.

El resultado indica asociación y no demuestra causalidad.

### H4 – Calificación y precio

- Prueba: correlación de Spearman
- n = **14.549**
- ρ = **0,046**
- p < **0,001**
- Decisión estadística: **rechazar H0**

**Interpretación:** aunque el resultado es estadísticamente significativo, el coeficiente de correlación es muy cercano a cero. Por lo tanto, la asociación entre calificación y precio es **muy débil** y no debe interpretarse como una relación de importancia práctica elevada.

Este resultado evidencia la importancia de analizar conjuntamente el valor p y el tamaño del efecto.

### H5 – Anfitriones con uno o varios anuncios

Las comparaciones se realizaron a nivel de anfitrión para evitar utilizar múltiples anuncios del mismo anfitrión como observaciones independientes.

| Indicador | p ajustado / decisión | Delta de Cliff |
|---|---|---:|
| Precio mediano | p < 0,001 – Rechazar H0 | 0,075 |
| Ocupación media estimada | p < 0,001 – Rechazar H0 | 0,185 |
| Reseñas promedio en 12 meses | p < 0,001 – Rechazar H0 | 0,213 |
| Calificación mediana | p < 0,001 – Rechazar H0 | -0,199 |

**Interpretación:** existen diferencias estadísticamente significativas entre anfitriones con un anuncio y anfitriones con varios anuncios en los cuatro indicadores evaluados.

Sin embargo, los tamaños de efecto muestran que la magnitud de las diferencias no es igual para todos los indicadores. Por lo tanto, la interpretación no debe limitarse únicamente a la significancia estadística.

---

## 10. Análisis de sensibilidad

Como control adicional se realizó un análisis exploratorio seleccionando aleatoriamente **un anuncio por anfitrión**, sin reemplazo, durante **100 iteraciones** y utilizando una semilla fija para reproducibilidad.

Este procedimiento **no corresponde a bootstrap ni a un intervalo de confianza**.

Resultados:

| Hipótesis | Iteraciones con p < 0,05 |
|---|---:|
| H1 | **100 / 100** |
| H2 | **100 / 100** |
| H3 | **100 / 100** |
| H4 | **96 / 100** |

Los resultados muestran una alta estabilidad de H1, H2 y H3 bajo este procedimiento. H4 mantiene significancia en la mayoría de las selecciones, pero presenta un efecto reducido, coherente con la correlación débil observada en el análisis principal.

---

## 11. Dashboard

El dashboard fue desarrollado en **Tableau** y se encuentra en:

`Dashboard/Airbnb_Bogota.twbx`

Las tablas preparadas específicamente para Tableau son:

- `resultados/anuncios_dashboard.csv`
- `resultados/anfitriones_dashboard.csv`

El proyecto incluye dos dashboards principales:

### 01 – Resumen ejecutivo

Orienta la lectura hacia los principales KPIs y resultados generales de la oferta Airbnb analizada.

### 02 – Exploración de precios

Permite analizar el comportamiento del precio y su relación con diferentes dimensiones y características del alojamiento.

Además de los dashboards, el proyecto genera figuras de apoyo para el informe y el video:

1. Precio mediano por localidad.
2. Distribución del precio.
3. Capacidad frente a precio.
4. Mapa de calor localidad × tipo de alojamiento.
5. Composición de la oferta.

Estas figuras se generan mediante:

`04_figuras_resumen.ipynb`

y se almacenan en:

`resultados/figuras/`

---

## 12. Principales hallazgos

A partir del análisis pueden destacarse los siguientes resultados:

1. **La localidad está relacionada con diferencias en el precio.**  
   La prueba de Kruskal-Wallis muestra diferencias estadísticamente significativas entre localidades.

2. **El tipo de alojamiento presenta una relación importante con el precio.**  
   H2 presenta un tamaño de efecto superior al observado en H1 y la comparación entre vivienda completa y habitación privada muestra una diferencia clara.

3. **La capacidad presenta una asociación positiva con el precio.**  
   La correlación de Spearman de aproximadamente 0,480 indica que los alojamientos con mayor capacidad tienden a presentar precios más altos.

4. **La calificación tiene una asociación muy débil con el precio.**  
   Aunque el valor p permite rechazar H0, el coeficiente ρ = 0,046 muestra que la magnitud de la asociación es mínima.

5. **Los anfitriones con varios anuncios presentan diferencias frente a los anfitriones con un solo anuncio.**  
   Se identifican diferencias significativas en precio, ocupación estimada, reseñas y calificación, aunque con distintos tamaños de efecto.

6. **La significancia estadística no debe analizarse de forma aislada.**  
   El caso de H4 demuestra que un valor p pequeño no implica necesariamente una relación fuerte o de gran importancia práctica.

---

## 13. Decisiones basadas en evidencia

Los resultados permiten plantear las siguientes decisiones analíticas:

- Para analizar o comparar precios de alojamientos, conviene segmentar por **localidad y tipo de alojamiento**, evitando utilizar únicamente un promedio general para toda Bogotá.
- La **capacidad** debe considerarse al comparar precios, porque presenta una asociación positiva relevante con esta variable.
- La **calificación no debería utilizarse de manera aislada como predictor del precio**, debido a la asociación muy débil encontrada.
- Los análisis relacionados con comportamiento del anfitrión deben distinguir entre anfitriones con un único anuncio y aquellos con varios anuncios.
- El uso conjunto de **KPIs, visualizaciones, valor p y tamaños de efecto** ofrece una interpretación más completa que el uso de una única medida estadística.

Estas decisiones se limitan al alcance del dataset y a la metodología utilizada en este proyecto.

---

## 14. Limitaciones

El análisis presenta las siguientes limitaciones:

1. Los datos corresponden a una **captura específica del 16 de septiembre de 2026**, por lo que describen el mercado representado en ese momento y no necesariamente su comportamiento en otros periodos.
2. Los datos analizados corresponden a publicaciones de Airbnb contenidas en la fuente utilizada y no representan necesariamente la totalidad del mercado formal e informal de alojamiento de Bogotá.
3. La relación entre variables se interpreta como **asociación** y no como causalidad.
4. La calificación no está disponible para todos los anuncios. El análisis H4 utiliza únicamente registros con calificación válida.
5. La ocupación incluida en el proyecto es una **estimación derivada de las variables disponibles** y no corresponde a información directa de reservas reales.
6. La eliminación de registros con precios nulos o identificados como atípicos modifica la población analítica respecto al archivo original.
7. Variables externas que pueden afectar el precio —por ejemplo, eventos, temporada, características internas no representadas o cambios de mercado— no necesariamente están incorporadas en el dataset utilizado.
8. La sensibilidad de un anuncio por anfitrión es un procedimiento exploratorio y no debe interpretarse como bootstrap ni como intervalo de confianza.

---

## 15. Conclusiones

El proyecto permitió transformar el dataset original de Airbnb Bogotá en una estructura analítica orientada a Business Intelligence y aplicar técnicas estadísticas para complementar la interpretación visual de los datos.

Los resultados muestran que el **tipo de alojamiento, la localidad y la capacidad** son variables relevantes al estudiar las diferencias observadas en el precio. Entre ellas, el tipo de alojamiento presenta un efecto importante en los contrastes realizados, mientras que la capacidad mantiene una asociación positiva con el precio.

Por otra parte, la calificación presenta significancia estadística, pero su asociación con el precio es muy pequeña. Este resultado demuestra que una conclusión no debe basarse exclusivamente en el valor p y que es necesario considerar también la magnitud del efecto.

Asimismo, se encontraron diferencias entre anfitriones con un solo anuncio y anfitriones con varios anuncios, especialmente en indicadores asociados con actividad, ocupación estimada y calificación.

En conjunto, los KPIs, las pruebas estadísticas, el análisis de sensibilidad y los dashboards permiten construir una lectura más completa de la oferta analizada. El proyecto evidencia que el uso integrado de técnicas de preparación de datos, estadística y visualización facilita la transformación de datos en información útil y comunicable para apoyar procesos de análisis y toma de decisiones.

---

## 16. Estructura del repositorio

```text
Evento-evaluativo-3-190304018-1/
│
├── datos/
│   └── listings_bogota.csv
│
├── salida_fase3/
│   ├── airbnb_bogota_analitico.csv
│   ├── anfitriones_resumen.csv
│   ├── anuncios_excluidos.csv
│   ├── calidad_variables.csv
│   ├── diccionario_datos.csv
│   ├── dim_anfitrion.csv
│   ├── dim_localidad.csv
│   ├── dim_tipo_alojamiento.csv
│   ├── fact_anuncios.csv
│   ├── informe_preparacion.json
│   ├── muestra_h1_localidad.csv
│   ├── muestra_h2_tipo_alojamiento.csv
│   └── registro_limpieza.csv
│
├── resultados/
│   ├── anuncios_dashboard.csv
│   ├── anfitriones_dashboard.csv
│   ├── comparaciones_anfitriones.csv
│   ├── descriptivos_H1.csv
│   ├── descriptivos_H2.csv
│   ├── dunn_holm_H1.csv
│   ├── dunn_holm_H2.csv
│   ├── hipotesis.csv
│   ├── kpis.csv
│   ├── resumen.json
│   ├── resumen_sensibilidad.csv
│   ├── sensibilidad_un_anuncio_por_host.csv
│   └── figuras/
│
├── Dashboard/
│   └── Airbnb_Bogota.twbx
│
├── 01_preparacion_datos.ipynb
├── 02_kpis_dashboard.ipynb
├── 03_contrastes_hipotesis.ipynb
├── 04_figuras_resumen.ipynb
├── bi_airbnb.py
└── README.md
```

---

## 17. Ejecución del proyecto

Para reproducir el análisis se recomienda ejecutar los notebooks en el siguiente orden:

```text
1. 01_preparacion_datos.ipynb
2. 02_kpis_dashboard.ipynb
3. 03_contrastes_hipotesis.ipynb
4. 04_figuras_resumen.ipynb
```

El primer notebook genera la base preparada y las tablas del modelo. Los notebooks posteriores dependen de estos archivos.

El archivo:

`bi_airbnb.py`

contiene funciones y configuraciones compartidas utilizadas por los notebooks.

---

## 18. Tecnologías utilizadas

- Python
- Jupyter Notebook
- Pandas
- NumPy
- SciPy
- Matplotlib
- Tableau
- Git
- GitHub

---

## 19. Reproducibilidad y trazabilidad

El proyecto incorpora diferentes mecanismos de control:

- registro de limpieza;
- tabla de anuncios excluidos;
- diccionario de datos;
- conteos de control;
- archivo de calidad de variables;
- SHA-256 de archivos utilizados;
- semilla fija para el análisis de sensibilidad;
- archivos CSV con los resultados de las pruebas estadísticas;
- separación entre datos preparados, resultados y visualizaciones.

Esto permite verificar las transformaciones realizadas y reproducir los principales resultados del análisis.

---

## 20. Archivos principales

| Archivo | Función |
|---|---|
| `01_preparacion_datos.ipynb` | Limpieza, transformación y modelado |
| `02_kpis_dashboard.ipynb` | Cálculo de KPIs y preparación para Tableau |
| `03_contrastes_hipotesis.ipynb` | Contrastes estadísticos y sensibilidad |
| `04_figuras_resumen.ipynb` | Figuras y resumen de resultados |
| `bi_airbnb.py` | Funciones compartidas |
| `Dashboard/Airbnb_Bogota.twbx` | Dashboard de Tableau |
| `resultados/kpis.csv` | Resultados de KPIs |
| `resultados/hipotesis.csv` | Resultados principales de pruebas |
| `resultados/resumen_sensibilidad.csv` | Síntesis del análisis de sensibilidad |

---

## 21. Alcance

Este repositorio corresponde al desarrollo académico del **Evento Evaluativo 3 de la asignatura Análisis de Datos, semestre 2026-2**, enfocado en el proyecto de **Airbnb** asignado al Equipo 10.

Los resultados deben interpretarse exclusivamente dentro del contexto, población, variables y metodología documentados en el proyecto.
