# 🏠 Real Estate Rental Analysis  
**NOTE**: Si quieres leer todo este texto en ESPAÑOL, puedes descargar el archivo .pptx o ver el README_ES.md 

This project is about an exploratory data analysis in the real estate sector, specifically in the rental sector. It considers three of Spain's largest cities: Madrid, Barcelona, ​​and Malaga.
Here, the cities are discussed both individually and collectively to understand how this sector is managed. The granularity varies, as we also consider all districts within each city.
### 🗃️ Data Used
The data was obtained through web scraping but anonymized for educational purposes. There are more than 7,000 rental listings across the three cities. For security reasons, the website used is not mentioned.
### 👾Resources Used
The entire project was developed in Python, using the following libraries: 🍵BeautifulSoup, 🚗Selenium, 📡Requests, ⏰time, 📊tqdm, 🧮NumPy, 🐼Pandas, 📅Datetime, 🎲Random, ➕Math, 🧪Scipy, 🔍Re, 📈matplotlib, 🌊seaborn, 🍃folium, 🗺️geopandas, and 🔄base64.
In addition to parts of the code in *JavaScript* and *HTML*, as this was necessary for part of the scraping and visualization of the choropleths.
## 1. 🕸️Complex Web Scraping
Challenges: The website detected and interrupted the search with Selenium, as it detected us as bots. The website loaded data as the user scrolled. A popup suddenly appeared in the middle of the screen while scraping was being performed.
Solutions: We implemented functions to simulate human behavior. We implemented automatic scrolling functions with JavaScript. We implemented code to switch between iframes and close the window.
Result: Obtained a DataFrame with __7889__ rentals combining Barcelona, ​​Madrid, and Malaga.
## 2. 🧹Advanced Outlier Debugging
Challenge: Outliers that altered the interpretation of the data.
Resolution: Defined a function to filter each variable by district, using parameter k = 2.5.
Result: Obtained a clean DataFrame of **7125** rentals (df_no_outliers).
## 3. 🛠️Effective Integration with Airtable
Challenges: Upload the entire DF to our Airtable table. Creating Automatic Columns in Airtable
Resolution: Generation of an Airtable class with two functions, one for uploading and one for downloading data.
Result: Automation of the data upload and download process.
## 4. 🔍Identifying Significant Variables
Challenges: Determine the significant variables for the analysis. Generate demonstrative graphs.
Resolutions: Heatmap by district to visualize the correlation of variables. Generation of the *cumulative correlation* function.
Result: The significant variables are rental_cost, dimension, rooms, bathrooms.
## 5. 📌Visualizations of Interest
### 5.1 🗺️Choropleth
Challenges: Generation of centroids through .json, Tooltip with custom barplots.
Resolutions: Introduction of the €/m² column. Use of the Geopandas library for centroids. Generation of barplots for Tooltip. Using HTML for Tooltips.
Conclusion: For the same district, €/m² and rental_cost behave differently. The closer the rent is to the city center, the higher the €/m².
### 5.2 📊Barplots
Challenges: Most common rentals by city, histograms with numerical variables, histogram normalization.
Resolutions: Histograms for each variable, binning for numerical variables, creating histograms based on data percentages rather than counts.
Conclusion: The most common rental property would be the one with the highest percentage for each barplot.
## 6. 💡 Statistical Conclusions
### 6.1 🧠ANOVA
The ANOVA test was performed for the analysis of districts (each city) and for the set of cities (three cities). The following results were obtained (for the three cities):
- F statistic: 28.53, indicating high variability between cities.
- p-value: ~0 (2.28e-48), rejecting the null hypothesis.
- Conclusion: Location (city and district) significantly affects rental prices.
### 6.2 🧮Mann-Whitney U
It was observed that there is a relationship between the publication date and the proportion of listings, with the proportion decreasing almost entirely in less than 100 days. Therefore, a t-test was performed, and since the test was not met, the Mann-Whitney U test was used, yielding the following results:
- MWU test: 4383461.0, p-value: 0.0003895436424678453.
- The null hypothesis μ_with_reduction ≠ is rejected. μ_without_reduction.
- Conclusion: The initial interpretation suggests that properties with discounts tend to be purchased more quickly, which could explain why they are more recent on the real estate platform.
## 7. 📱Data-Driven Applications
Two functions were implemented:
- rental_house_investment: where the desired investment is entered and in which city, this will return the rentals with the best features that fit that investment.
- chollos: where a city is entered, districts can be specified, and a k-value, which will describe how much you want the variation in values ​​to be. This will return a series of rentals with scores of 5, 7, and 10, from worst offer to best offer.
NOTE: For both functions, only the values ​​contained in the chosen DataFrame were used.




