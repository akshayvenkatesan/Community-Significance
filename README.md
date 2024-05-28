# Value or Significance Scores of Places

## Abstract

This project embarks on an innovative journey to quantify the cultural and sentimental value of various places within urban communities. Recognizing that traditional economic metrics often overlook the profound influence these places have on shaping community culture and sentiment, our study introduces a novel metric. Utilizing a comprehensive dataset of approximately 230,000 locations across New York State, sourced from Google local reviews, along with demographic and socio-economic data from the US Zip Code Database, we develop a multifaceted approach to capture the essence of places. Our methodology integrates data preprocessing, feature engineering, and advanced clustering techniques to construct scores reflecting community significance, popularity, and engagement. The findings, derived from sophisticated machine learning models, reveal insightful patterns in the cultural fabric of New York communities, highlighting both endangered and significant places. This report presents a groundbreaking framework with substantial implications for urban planning and community preservation.

## 1. Introduction

In the evolving landscape of urban development, local businesses and cultural establishments play a crucial role in shaping the character and sentiment of communities. From bustling cafes and historical bookstores to serene parks and vibrant community centers, these places are more than mere economic entities; they are the heart and soul of neighborhoods, fostering unique experiences and memories. However, the rapid pace of urbanization and economic shifts often pose significant challenges to these establishments, threatening the very cultural tapestry they weave.

This project, therefore, seeks to fill a critical gap by developing a robust metric that quantifies the cultural and sentimental value of these places. By moving beyond conventional economic assessments, the project aims to offer a more holistic view of the impact of local businesses and places, providing essential insights for urban planning, community preservation, and policy-making. This comprehensive approach is particularly vital in the context of New York State, a diverse and dynamic region with a rich tapestry of communities, each with its unique cultural footprint.

## 2. Experimental Setup

### 2.1 Data Acquisition

**Google Review Dataset**: A detailed compilation from Google local reviews, covering approximately 230,000 locations across New York State with around 13 million reviews from 2021. This dataset, bifurcated into review data and metadata, encompasses user reviews and detailed business information including geographical coordinates, average ratings, and operational aspects.

| Field       | Description                        |
|-------------|------------------------------------|
| User ID     | ID of the reviewer                 |
| Name        | Name of the reviewer               |
| Time        | Time of the review                 |
| Rating      | Numerical rating                   |
| Text        | Detailed text of the review        |
| Response    | Business responses to the review   |
| GMap ID     | Unique identifier for the business |

Table 2.1: Review Data Structure

| Field       | Description                        |
|-------------|------------------------------------|
| Name        | Name of the business               |
| Address     | Physical address                   |
| GMap ID     | Unique identifier                  |
| Description | Brief about the business           |
| Latitude, Longitude | Geographical coordinates   |
| Category    | Type of the business               |
| Avg Rating  | Average rating                     |
| Num of Reviews | Total number of reviews         |
| Price       | Price range                        |
| Hours       | Operational hours                  |
| MISC        | Miscellaneous information          |
| State       | Operational status                 |
| Relative Results | Other businesses              |

Table 2.2: Metadata Structure

**US Zip Code Database**: This dataset is a crucial asset, providing essential information on zip code population density, median household income, geographic shape, and median age. Its inclusion significantly enhances our analysis, offering valuable demographic and socio-economic context. These additional insights into regional characteristics are indispensable for a nuanced assessment of business significance. By combining this dataset with the Google Review Dataset, we gain a more comprehensive understanding of regional dynamics.

| Field             | Description                        |
|-------------------|------------------------------------|
| Median Income     | Median income of households        |
| Poverty Percentage| % of people in poverty             |
| Population        | Population of the county           |
| Latitude, Longitude | Geographical coordinates         |
| County Name       | Name of the County                 |

Table 2.3: US Zip Code Data Structure

### 2.2 Data Pre-Processing

The data preprocessing stage was pivotal in ensuring the integrity and quality of our analysis. Key steps included:

- **Duplicate Elimination**: Removing duplicate reviews to avoid data redundancy.
- **Normalization**: Standardizing disparate rating scales to a consistent metric.
- **Categorization**: Creating broad, coherent categories from fragmented initial classifications.
- **Natural Language Processing (NLP)**: Applying NLP techniques, specifically stemming and lemmatization, to distill review texts to their root forms.
- **Data Structuring**: Parsing JSON-formatted response texts into structured data columns.

### 2.3 Feature Engineering

Our feature engineering process involved developing several innovative metrics:

- **Community Significance Score**: This score quantifies the communal impact of businesses through customer reviews. We established a lexicon of keywords reflecting community values. The review texts were vectorized, converting them into a numerical format suitable for analysis. Utilizing a cosine similarity measure with a threshold over 0.5, we highlighted reviews resonating with our community value keywords.

- **Popularity Score**: Derived from the average ratings and the volume of reviews a business receives.

![Figure 2.1: Heatmap for Distribution of Popularity Scores across NY](images/heatmap_popularity.png)

Figure 2.1: Heatmap for Distribution of Popularity Scores across NY

- **Engagement Score**: Calculated from the frequency and promptness of a business’s responses to reviews.

- **Weekly Operational Hours**: Quantified by summing up the total hours of operation across all days of the week.

- **Business Age**: Reflects the establishment’s longevity.

## 3. Methodology

### 3.1 Calculating Significance Score

Scoring Methodology:
- **Principal Component Analysis (PCA)**: Applied to the dataset to identify patterns and dependencies among features.

| Component | Avg Rating | Avg Sent. | Op. Hours | Op. Dur. | Pop. Score | Comm. Sign. Score | Eng. Score | Pop. Census | Med. Income |
|-----------|------------|-----------|-----------|----------|------------|-------------------|------------|-------------|-------------|
| PC1       | 0.4255     | 0.3688    | -0.0568   | 0.3240   | 0.6013     | 0.4368            | 0.1230     | -0.0491     | 0.0693      |
| PC2       | -0.4494    | -0.4567   | 0.3417    | 0.4208   | 0.1747     | 0.3651            | -0.1289    | 0.3117      | 0.1343      |
| ...       | ...        | ...       | ...       | ...      | ...        | ...               | ...        | ...         | ...         |

Table 3.1: PCA Components and Explained Variance

Calculation of Feature Weights:
- The weights for each feature were then normalized to sum to 1.

Calculation of Composite Score:
- The composite score (S) for each observation was computed as a weighted average of the features.

### 3.2 Identifying Endangered Places

#### Model Selection and Evaluation

- **Random Forest Regressor and LightGBM**: Initial attempts involved using these models but did not yield the desired level of accuracy and interpretability.

- **TabNet**: Developed by Google Cloud AI, its architecture is uniquely suited for tabular data.

## 4. Results

### 4.1 Top Significant Places

The analysis of significance scores for local communities reveals the top places in New York City and New York State that hold the greatest cultural and sentimental value. As detailed in Table 4.1, Bryant Park leads with a perfect score, reflecting its central role in the social and recreational life of the city. Other prominent NYC landmarks, such as The Museum of Modern Art and Chelsea Market, also feature high on the list, indicating their importance in the cultural landscape. Similarly, Table 4.2 showcases significant places outside NYC, with Green Acres Mall in Nassau County and Woodbury Premium Outlets in Orange County standing out as key community centers. These findings underscore the diversity of places that contribute to the richness of New York’s cultural fabric and the need for their preservation and continual support.

| Business Name                  | Significance Score |
|--------------------------------|--------------------|
| Bryant Park                    | 100.000000         |
| The Museum of Modern Art       | 83.450599          |
| Chelsea Market                 | 81.448499          |
| Washington Square Park         | 80.518487          |
| Macy’s                         | 79.921750          |
| Intrepid Sea, Air & Space Museum | 79.444371        |
| Bronx Zoo                      | 79.401760          |
| Prospect Park                  | 77.011062          |
| Flushing Meadows Corona Park   | 75.215187          |
| Katz’s Delicatessen            | 75.000147          |

Table 4.1: Most Significant Places in NYC

| Business Name                  | County        | Significance Score |
|--------------------------------|---------------|--------------------|
| Green Acres Mall               | Nassau County | 69.132486          |
| Woodbury Premium Outlets       | Orange County | 66.174433          |
| Roosevelt Field                | Nassau County | 60.669074          |
| Turning Stone Resort Casino    | Oneida County | 59.269109          |
| Walmart Supercenter            | Nassau County | 58.766980          |
| Palisades Center               | Rockland County | 56.355188        |
| Tanger Outlets Deer Park       | Suffolk County | 56.254927        |
| Jones Beach State Park         | Nassau County | 55.880083          |
| Cross County Center            | Westchester County | 54.234180     |
| The Strong Museum              | Monroe County | 52.126121          |

Table 4.2: Top Significant Places Outside NYC

### 4.2 Top Endangered Places

Our analysis, powered by TabNet’s closure probability predictions, identified a list of the top endangered places based on 2021 data. A recent follow-up on these predictions reveals a significant validation of our model’s accuracy. Notably, the majority (65%) of these places have indeed closed, underscoring the effectiveness of our approach in identifying at-risk establishments.

![Figure 4.1: Significance Score Spread by Category](images/significance_score_spread.png)

Figure 4.1: Significance Score Spread by Category

| Business Name                  | Closure Probability | Current Status |
|--------------------------------|---------------------|----------------|
| Parma                          | 0.976403            | Rebranded      |
| Ginza                          | 0.969889            | Closed         |
| Sushi A La Kawa                | 0.969886            | Closed         |
| Hannah’s Beauty Salon          | 0.968119            | Closed         |
| Dragon One                     | 0.967158            | Open           |
| David Geffen Hall Café         | 0.966901            | Closed         |
| U-Haul at Fort Drum            | 0.965514            | Open           |
| Chick’nCone                    | 0.965198            | Closed         |
| Domino’s Pizza                 | 0.964584            | Open           |
| American Apparel               | 0.964368            | Closed         |
| Blo Blow Dry Bar               | 0.962631            | Closed         |
| Rosina                         | 0.961769            | Closed         |
| Dunkin’                        | 0.960580            | Open           |
| Southside Chubby’s             | 0.958895            | Closed         |
| Taiji Body Work                | 0.958853            | Open           |
| Chipotle, 10th Ave             | 0.958280            | Open           |
| Chipotle, 12th St              | 0.958245            | Closed         |

Table 4.3: Top Endangered Places

### 4.3 Observations

#### 4.3.1 Category Wise Analysis

Significance Score Spread by Category: The boxplot in Figure 4.1 illustrates the distribution of significance scores across various business categories, reflecting their cultural and sentimental value within the community. The median of each box signifies the central tendency, while the box length indicates the interquartile range, showing the consistency of scores within categories. Outliers, depicted as diamonds, represent businesses with exceptional value, particularly noticeable in ‘Beauty and Personal Care’ and ‘Restaurants and Eateries’. These categories also exhibit a higher median and wider score distribution, underscoring their vital role in community life. Conversely, ‘Educational Institutions’ and ‘Accommodation and Travel’ have lower median scores, suggesting a more uniform impact. This visualization provides essential insights for stakeholders in urban planning and cultural preservation, revealing which business categories are integral to the community.

Endangerment by Category: The bar graph in Figure 4.2 provides a compelling visual representation of the varying degrees of endangerment across different business categories. Restaurants and eateries lead by a significant margin, indicating their vulnerability to closure, which may reflect changing social habits or economic pressures. Retail and shopping venues follow, suggesting a transition perhaps driven by the rise of e-commerce. Notably, categories such as bars and nightlife, and food markets and groceries also show a substantial number of closures, underscoring the broad impact of recent trends and challenges across sectors. Meanwhile, categories like educational institutions, religious and spiritual places, and public and government services report fewer closures, which may point to their foundational role in community stability. This visualization is critical for understanding which sectors are most at risk and may benefit from targeted interventions to preserve the local community’s cultural and economic landscape.

![Figure 4.2: Closed Places by Category](images/closed_places_category.png)

Figure 4.2: Closed Places by Category

#### 4.3.2 Profile Comparison of Open and Closed Places

The radar chart in Figure 4.3 contrasts the characteristics of open and closed places across multiple metrics, providing insights into the factors that may affect a place’s operational status.

- **Average Rating**: Closed places may exhibit higher average ratings, possibly due to a loyal but limited customer base or a surge of support prior to closure.
- **Popularity Score**: This metric suggests that sustained popularity is crucial for ongoing operations, as open places typically score higher on this axis.
- **Community Significance Score**: A higher score for open places indicates that community attachment significantly contributes to a business’s success.
- **Engagement Score**: Higher engagement scores for open places suggest that active customer interaction is beneficial for business continuity.
- **Operational Duration and Weekly Operational Hours**: Longer operational histories and more extensive weekly hours are indicative of established loyalty and accessibility, key for operational places.
- **Final Value Score**: Open places with higher final significance value scores offer more overall value, which is critical for their survival and success.

![Figure 4.3: Radar Chart Comparing Open and Closed Places](images/radar_open_closed.png)

Figure 4.3: Radar Chart Comparing Open and Closed Places

#### 4.3.3 High Significance and Endangerment of Places

Our analysis reveals a noteworthy trend among the endangered places in New York City and the state. Places with a closure probability greater than 0.5 tend to have lower significance scores. This pattern indicates that places which are highly significant to their communities generally do not close as easily. This observation underscores the resilience of culturally and socially important establishments, as they are more likely to withstand various challenges compared to those with lesser community significance.

| Business Name                   | Significance Score | Closure Probability |
|---------------------------------|--------------------|---------------------|
| Flex Mussels                    | 39.76              | 0.516               |
| Barrio Chino                    | 39.25              | 0.598               |
| Bouley at Home                  | 39.16              | 0.668               |
| Salumeria Rosi                  | 39.08              | 0.511               |
| Bobby Van’s                     | 38.56              | 0.706               |

Table 4.4: Top 5 Significant Endangered Places in NYC

| Business Name                   | Significance Score | Closure Probability |
|---------------------------------|--------------------|---------------------|
| Book Warehouse, Suffolk County  | 35.09              | 0.518               |
| Sweetwaters Coffee, Suffolk County | 34.72           | 0.569               |
| Jagermeister Deli, Nassau County| 34.68              | 0.546               |
| Island Poke, Nassau County      | 33.93              | 0.516               |
| The Winemaker Studio, Suffolk County | 33.89          | 0.55                |

Table 4.5: Top 5 Significant Endangered Places in NY State

## 5. Conclusion

This study embarked on a multifaceted journey to understand and preserve the cultural and social fabric of New York City and its surrounding areas. By employing advanced data analytics techniques, we were able to uncover the significant places that form the backbone of local communities, both within the city and in the broader New York State.

Our methodology combined the robustness of Principal Component Analysis (PCA) to weight and evaluate various features of local businesses and establishments, with the predictive power of the TabNet model to identify places at risk of closure. The PCA provided a nuanced understanding of the factors contributing to the cultural and sentimental significance of places, while the TabNet model offered a forward-looking perspective on potential closures, enabling proactive measures for preservation.

The results from our analysis are twofold: First, we identified the top significant places, highlighting iconic landmarks such as Bryant Park and The Museum of Modern Art in NYC, and places like Green Acres Mall and Woodbury Premium Outlets outside the city. These findings underscore the diverse range of locations that are cherished by the community, enriching the cultural landscape of New York.

Second, our predictive analysis revealed a list of endangered places, pinpointing establishments at high risk of closure. This list not only validated the accuracy of the TabNet model but also provided critical insights for stakeholders. The closure of many predicted places underscores the urgency and importance of targeted interventions to support these community hubs.

The study highlights the dynamic nature of urban spaces, where businesses and places of social gathering are constantly evolving. While some establishments have shown resilience and adaptability, others have succumbed to various pressures, reflecting the complex interplay of social, economic, and cultural factors.

In conclusion, our research offers a valuable framework for understanding and preserving the cultural heritage embedded in urban landscapes. It demonstrates the potential of data-driven approaches in informing urban planning and policy decisions, ensuring that the heart of communities—their significant places—is recognized, supported, and sustained. As cities continue to evolve, such analytical tools will be instrumental in maintaining the vibrancy and diversity that define them.

## 6. Future Works

In our future work, we aim to harness additional funding and computational resources to enhance the robustness and accuracy of our predictive model. One pivotal step will be to integrate real-time data by tapping into the Google Places API. This will enable us to validate and refine our model with the latest information on various places, providing us with a richer dataset for more nuanced analysis. Moreover, we plan to explore a broader spectrum of neural network architectures, delving into the potential of advanced deep learning techniques to identify at-risk cultural landmarks more effectively. Concurrently, we will undertake extensive hyperparameter tuning of our existing TabNet model to optimize its performance. These efforts, bolstered by greater resources, are expected to yield significant improvements in our model’s predictive capabilities, contributing substantially to the preservation of community culture and heritage.

## 7. References

1. J. Li, J. Shang, and J. McAuley, “Uctopic: Unsupervised contrastive learning for phrase representations and topic mining,” in Annual Meeting of the Association for Computational Linguistics (ACL), 2022. [Online]. Available: https://arxiv.org/pdf/2207.00422.pdf.

2. A. Yan, Z. He, J. Li, T. Zhang, and J. McAuley, “Personalized showcases: Generating multi-modal explanations for recommendations,” in The 46th International ACM SIGIR Conference on Research and Development in Information Retrieval (SIGIR), 2023. [Online]. Available: https://arxiv.org/pdf/2207.00422.pdf.

3. New york population density zip code rank, http://www.usa.com/rank/new-york-state--population-density--zip-code-rank.htm.

4. Economic and business activity data from new york state government websites.

5. Esri, Performing principal component analysis (pca) to determine weights for index indicators, https://www.esri.com/arcgis-blog/products/api-python/analytics/performing-principal-component-analysis-pca-to-determine-weights-for-index-indicators/, [Online; accessed 11-28-2023], Accessed: 2023.

6. Dreamquark AI, Tabnet: Attentive interpretable tabular learning, https://github.com/dreamquark-ai/tabnet, [Online; accessed 11-28-2023], Accessed: 2023.
