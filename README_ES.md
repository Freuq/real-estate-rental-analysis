# 🏠 Real Estate Rental Analysis
Este proyecto es sobre un análisis exploratorio de datos en el área de bienes raíces, en especial en el sector de alquileres. Donde se toman en cuenta tres de las ciudades más grandes de España, las cuales son Madrid, Barcelona y Malaga.
Aquí se tratan las ciudades en conjunto y por separado para vemos cómo se maneja este sector, la granularidad va variando ya que también tomamos en cuenta todos los distritos de cada ciudad.
### 🗃️Datos utilizados
Los datos fueron obtenidos por medio de web scraping pero anonimizados para su uso educativo, hay más de 7000 datos de alquileres entre las tres ciudades. Por motivos de seguridad no se menciona cual fue la web utilizada.
### 👾Recursos utilizados
Todo el proyecto fue realizado en Python, utilizando las librerías: 🍵BeautifulSoup, 🚗Selenium, 📡Requests, ⏰time, 📊tqdm, 🧮NumPy, 🐼Pandas, 📅Datetime, 🎲Random, ➕Math, 🔍Re, 📈matplotlib, 🌊seaborn, 🍃folium, 🗺️geopandas y 🔄base64.  
Además de partes en código en *JavaScript* y *HTML*, ya que fue necesario para una parte del scraping y la visualización de los choropleths.  
## 1. 🕸️Web Scraping Complejo
Desafíos: La web detectaba e interrumpia la busqueda con Selenium, ya que nos detectaba como bots. Ka web cargaba los datos a medida que se realizaba el scroll. Aparición repentina de un popup en el medio de la pantalla mientras se realizaba el scraping.
Soluciones: Implementamos funciones para similar un comportamiento humano. Implementamos funciones apra scroll automático con javascript. Implementamos código para cambiar de iframe y lograr cerrar la ventana.
Resultado: Obtención de un DataFrame con __7889__ alquileres juntando Barcelona, Madrid y Málaga.  
## 2. 🧹Depuración avanzada de Outliers
Desafío: Valores atípicos que alteraban la interpretación de los datos.  
Resolución: Definición de función para filtrado de cada varaible por distrito, utilizando parámetro k= 2.5.  
Resultado: Obtención de un DataFrame limpio de **7125** alquileres (df_no_outliers).  
## 3. 🛠️Integración efectiva con Airtable  
Desafíos: Realizar la subida de todo el DF a nuestra tabla de Airtable. Creación de columnas automáticas en Airtable  
Resolución: Geenración de una clase Airtable con dos funciones, una de subida y otra de bajada de datos.  
Resultado: Automatización de proceso de subida y descarga de datos.  
## 4. 🔍Identificación de variables significativas
Desafíos: Determinar las varaibles significativas para el análisis. Generación de gráficas demostrativas.
Resoluciones: Heatmap por distrito para visualizar la correlación de variables. Generación de la función de *correlación acumulada*
Resultado: Las variables significativas son rental_cost, dimension, rooms, bathrooms.  
## 5. 📌Visualizaciones de interés
### 5.1 🗺️Choropleth
Desafíos: Generación de centroides a través de .json, Tooltip con barplots customizados.
Resoluciones: Introducción de la columna €/m². Utilización de la librería geopandas para centroides. Generación de barplots para Tooltip. Utilización de HTML para Tooltip.  
Conclusión: Para un mismo distrito el €/m² y rental_cost se comportan diferente. Mientras más cercano al centro de la ciudad se encuentre el alquiler, más alto es el €/m².
### 5.2 📊Barplots  
Desafíos: Alquiler más común por ciudad, histogramas con variables numéricas, normalización de histogramas.  
Resoluciones: Histogramas de cada variable, Binning para variables numéricas, realizar histogramas a partir de porcentaje de datos y no conteo.
Conclusión: La vivienda en alquiler más común sería la de mayor porcentaje para cada barplot.
## 6. 💡Conclusiones estadísticas
### 6.1 🧠ANOVA 
Se realizó la prueba de ANOVA para el análisis de distritos (cada ciudad) y para el conjunto de ciudades (tres ciudades). Arrojando lo siguiente (para las tres ciudades:
- Estadístico F: 28.53, indica gran varaiblidad entre ciudades.
- Valor p: ~0 (2.28e-48), rechaza la hipótesis nula.
- Conclusión: La ubicación (ciudad y distrito) afecta significativamente los precios de alquiler.
### 6.2 🧮Mann-Whitney U
Se observo que existe una relación entre la fecha de publicación y la proporción de anuncios, donde la proporción disminuye por casi su totalidad en menos de 100 días. Siendo así, se realizó un análisis con la prueba t y al no cumplirse se utilizó la U de Mann-Whitney, arrojando lo siguiente:
- Contraste de MWU: 4383461.0, valor p: 0.0003895436424678453.
- Se rechaza la hipótesis nula μ_with_reduction ≠ μ_without_reduction.
- Conclusión: La interpretración inicial sugiere que las propiedades con rebajas tienden a ser compradas más rápidamente, lo que podría explicar por qué son más recientes en la plataforma inmobiliaria.
## 7 📱Aplicaciones basada en datos  
Se realziaron dos funciones:
- rental_house_investment: donde se incluye la inversión que se quiere hacer y en qué ciudad, y esto proporcionará los alquileres con mejores características que entren en esa inversión.
- chollos: donde se coloca una ciudad, se puede especificar distritos y una varlo k, que describirá de cuanto quieres que sea la variación de los valores. Esto devolverá una serie de alquileres con puntuación 5, 7 y 10, de peor oferta a mejor oferta.
NOTA: Para ambas funcioens únicamente s eutilizaron los valores que se contengan en el DataFrame de elección. 