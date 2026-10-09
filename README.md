[🇺🇸 English](README.md) | [🇧🇷 Português](README-pt.md)

# Infant Mortality in Acre and Its Determinants (2022)
### Spatial and Statistical Analysis of Infant Mortality in Acre (2022) - A study of socioeconomic conditions and access to public services
![capa](capa.png)
---

## 1. Context and Objective
- The investigation of infant mortality in Acre highlights the critical dimension of the social and territorial determinants of health in Brazil. According to the Childhood and Adolescence Scenario in Brazil report (Fundação Abrinq, 2026), the North Region had the highest infant mortality rate in 2024, recording 15.7 deaths per thousand live births, in stark contrast to the South Region, which presented the lowest indicator in the country (10.4 per thousand). Given this significant macro-regional disparity, the state of Acre serves as a strategic geographic scope to analyze the socio-spatial correlations and determinants acting as aggravating or protective factors for infant survival in the Amazon.
- Eight indicators were engineered using public datasets from IBGE, DATASUS, and the Ministry of Health, integrated within a Geographic Information System (GIS) environment. The analysis employed the Pearson correlation coefficient and the production of bivariate choropleth maps, cross-referencing infant mortality with GDP per capita, geographic accessibility, maternal education, and prenatal care coverage.
- To execute this project, I used QGIS for mapping and spatial analysis, PostgreSQL for database engineering, and Excel for data wrangling. The "Bivariate Legend" plugin was utilized to generate the 3x3 matrix legends.
- This study was developed as the Final Project for the Geographic Information Systems course in the Environmental Analysis and Territorial Management Postgraduate Program (ENCE/IBGE), presented as a monograph. Furthermore, the research is in the final drafting stages for submission as a scientific paper.
- This project was a collaborative effort with Geographer [Gabriel Silva (@santosgabrielma)](https://www.linkedin.com/in/santosgabrielma/), a postgraduate classmate at ENCE/IBGE, who was responsible for the Pearson correlations, official data analysis, and presentation/monograph drafting. I was responsible for database engineering and correction (Excel and SQL), indicator synthesis, spatial data analysis, and cartography in QGIS.
---

## 2. Study Area and Selected Indicators
![Indicadores](RecortIndicadores.jpg)

- **Spatial Scope:** Municipalities of the State of Acre, Brazil.
- **Reference Year:** 2022.
- The selection of indicators was neither arbitrary nor exclusively determined by data availability. It is grounded in the Social Determinants of Health (SDOH) framework, defined by the National Commission on Social Determinants of Health (CNDSS) as the social, economic, cultural, ethnic/racial, psychological, and behavioral factors influencing the occurrence of health issues and their risk factors in the population (BUSS; PELLEGRINI FILHO, 2007).
- This framework directly guided the choice of the eight indicators applied here. Brazilian literature reviews on infant mortality consistently identify prenatal care and maternal education within the "living and working conditions" layer, and basic sanitation and income within the "general socioeconomic and environmental conditions" layer.
- The indicators utilized were:
  - **Infant Mortality Rate (IMR):** (Deaths under 1 year of age ÷ Live births) × 1,000, by residence; Source: DATASUS (SIM and SINASC, 2022).
  - **Municipal GDP per Capita:** Total municipal GDP ÷ resident population; Source: IBGE/SIDRA, 2022 Census.
  - **Adequate Sanitation Coverage:** % of households connected to the general distribution network as the primary method; Source: IBGE 2022 Census.
  - **Potential Primary Healthcare (PHC) Coverage:** (No. of teams × population parameter per team) ÷ municipal population × 100; Source: e-Gestor Atenção Básica (Dec/2022).
  - **Maternal Education:** (No. of mothers in education bracket ÷ Total mothers) × 100; Source: DATASUS/SINASC (2022).
  - **Prenatal Care Coverage:** (No. of mothers in consultation bracket ÷ Total mothers with registered prenatal care) × 100; Source: DATASUS/SINASC (2022).
  - **Geographic Accessibility Distance & Classification:** Calculation of travel cost in minutes via the multimodal network (road, river, and air) to the nearest reference urban center in the REGIC hierarchy; Source: IBGE, Geographic Accessibility Index (2018), *refined by the team*.
---

## 3. Statistical Analysis
![Estatísticas](correlacoes.jpg)

- To address the research question, the Pearson correlation coefficient ($r$) was calculated between pairs of variables, alongside their respective p-values, adopting a 5% significance level ($p < 0.05$). The Pearson coefficient measures the strength and direction of the linear relationship between two quantitative variables, ranging from -1 to 1:
  - **Positive Correlation ($r > 0$):** Both variables increase together.
  - **Negative Correlation ($r < 0$):** As one variable increases, the other decreases.
  - **Zero ($r = 0$):** No linear relationship exists between the variables.
  - **Intensity:** The closer to 1 or -1, the stronger the association.
    
- This study identified that adequate prenatal care coverage and maternal education present a significant and more robust association with infant mortality than municipal economic capacity alone. Adequate prenatal care coverage, in particular, constitutes the second strongest finding of the entire study ($r = -0.65; p = 0.001$), surpassed only by the association between geographic distance and GDP per capita.
- An additional finding stands out: geographic isolation, which strongly explains municipal economic capacity, does not robustly explain access to prenatal care ($r = -0.11$; $p = 0.619$) nor conclusively explain maternal education ($r = -0.42$; $p = 0.050$, at the threshold of significance). This suggests that access to maternal care in Acre responds to determinants distinct from mere geographic distance, possibly related to local organization and health services management.
---

## 4. Databases and Spatial Analysis

- The database organization followed four stages:
  - Standardization and tabular data wrangling in Excel and R;
  - Using PostgreSQL/PostGIS syntax within the Field Calculator to engineer new attribute columns containing the epidemiological and statistical formulas for the indicators cited in Section 2;
  - Spatial Joins with the municipal geospatial boundaries using the IBGE municipal code;
  - Definition of the classification method and cartographic symbology - utilizing bivariate choropleth maps;
  - Statistical analysis of Pearson correlation and significance ($p < 0.05$) among indicators.

- For the joint spatial analysis of health determinants, bivariate choropleth maps were developed cross-referencing the infant mortality rate with five study covariates: GDP per capita, potential PHC coverage, geographic accessibility, maternal education, and prenatal care coverage. In this step, each indicator was divided into terciles—low, medium, and high—forming a matrix legend with nine color classes (3×3). Therefore, the method applied in the bivariate maps is the tercile classification.
- The tables were consolidated into a single master dataset, utilizing the municipality code as the common join key across all sources. The result is an attribute table with 22 rows and one column per indicator, imported and processed directly in QGIS. Since raw data was used, much of the information was in absolute numbers. To prevent errors, several corrections were made to the database using the native QGIS Field Calculator in a SQL environment to synthesize and organize the data for indicator creation and subsequent map rendering. 
- The master dataset was joined to the official IBGE municipal grid for the state of Acre. Cartographic products were elaborated using the Universal Transverse Mercator (UTM) projection, SIRGAS2000 Datum, Zone 19 South.
  - The attribute table is available for download at: [Tabela de atributos AC(2022).csv](./Tabela%20de%20atributos%20AC(2022).csv)
  - The Data Dictionary is available at: [Dicionário de Dados.pdf](./Dicion%C3%A1rio%20de%20Dados.pdf)

---

## 5. Bivariate Choropleth Maps

**Despite the various indicators researched and synthesized, only those that presented statistical correlation and significance were mapped.**

### 5.1 GDP per capita and Geographic Accessibility
![pibacess.png](Mapa_PIB_AcesGeo.jpg)

- The findings reveal two independent explanatory axes for infant mortality in Acre: the territorial-economic axis and the maternal care axis. While geographic isolation strongly dictates municipal economic capacity ($r = -0.67$; $p = 0.001$), contrasting the accessible, higher-GDP East with the remote, lower-GDP West, it does not directly explain health outcomes. Conversely, prenatal care coverage and maternal education robustly and directly explain infant mortality, demonstrating that determinants of gestational health care follow an autonomous territorial logic independent of physical distance to urban hubs.
  - Unlike the following maps, this one appears more homogeneous due to the predominance of colors from the extreme X or Y axes, visually highlighting the statistical finding.

### 5.2 IMR and Maternal Education
![cmiescolaridade.png](Mapa_CMI_EscolMaterna.jpg)

- There is a clear inversion of polarity in the Pearson coefficient ($r$): while low education (1 to 3 years of study) shows a moderate positive correlation with IMR ($r = +0.49$; $p = 0.022$), indicating that lower instruction exacerbates infant death rates, high education ($\ge 12$ years) exhibits a negative correlation ($r = -0.46$; $p = 0.032$), demonstrating a protective effect where higher maternal instruction is directly associated with reduced infant mortality in the territory.

### 5.3 IMR and Prenatal Care Coverage
![cmiprenat.png](Mapa_CMI_Prenatal.jpg)

- Inadequate coverage (1 to 3 visits) exhibited the highest positive correlation of the entire study ($r = +0.70$; $p = 0.001$), proving that insufficient consultations directly elevate the risk of infant death. Meanwhile, adequate coverage (7 or more visits) presented a strong negative correlation ($r = -0.65$; $p = 0.001$), confirming that complete gestational care exerts a powerful protective effect in reducing territorial mortality.
  - **Key Finding:** Adequate prenatal care coverage and maternal education correlate strongly with each other ($r = 0.63$; $p = 0.002$), suggesting both share common determinants, possibly related to the families' social and informational capital.

---

## 6. Conclusion

- Infant Mortality in Acre must be analyzed multidimensionally; no single indicator is sufficient to explain the rise or fall of the IMR. The findings demonstrated that adequate prenatal coverage (seven or more visits) and mothers completing high school (twelve or more years of education) showed a significant association with IMR. Adequate prenatal care coverage, in particular, represents the second strongest finding of the study ($r = -0.65$; $p = 0.001$), surpassed only by the association between distance and GDP per capita.
- The primary contribution of this research is twofold. First, it confirms that territorial organization and accessibility to reference urban centers constitute a relevant dimension for understanding economic inequalities in Acre. Second, it reveals that determinants directly linked to maternal health care—prenatal coverage and education—explain infant mortality more robustly than municipal economic capacity, and that these determinants follow a logic relatively independent of geographic distance.
  - **Main limitations include:** the small sample size ($n = 22$ municipalities), which restricts the statistical power of the correlation tests; the lack of formal sanitation data for most municipalities in the SNIS, requiring substitution with census data of a different methodology; the nature of the PHC coverage indicator, which measures installed capacity rather than effective service delivery; and the cross-sectional and ecological nature of the analysis, precluding causal or individual inferences.
  - **Future Research Agenda:** Expanding the time series for longitudinal analysis, investigating factors of municipal management and local health service organization that might explain prenatal coverage more directly than geographic distance, and applying multiple regression models to simultaneously control the effect of all analyzed variables.

---

## 7. Bibliography and Geopackage
![bibliografia.jpg](Bibliografia.jpg)

- For those wishing to dive deeper into the topic, the bibliography used to develop this research is provided.
- The zipped Geopackage containing all files is available [here](mort_infantil_AC2022.7z). Feel free to reproduce it in your preferred GIS environment, but please cite the source if used publicly.

### **Thank you!**
