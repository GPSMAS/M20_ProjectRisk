### Project Title

**Gianpiero Sepe**

#### Executive summary

The application aims to create a tool to assess the risk level of publicly funded projects, enabling greater attention to those at risk of significant delays, failure to close within the program's timeframe, or underutilization of allocated funds. Funds that remain unused could otherwise be redirected to other projects beneficial to the community.

To achieve this, we start with a dataset of projects concluded by December 31, 2023 (at the latest) from the 2014–2020 funding period, as these data should now be stable. This dataset will be used to train the model, which will then be applied to new projects from the 2021–2027 funding period.

Numerous inconsistencies were identified in the available information, necessitating the use of data engineering techniques to adapt the data. Most of the available information is categorical, resulting in a large volume of data for training. Consequently, it is essential to adapt these data to reduce the training time for the model.

Additionally, the training dataset is highly imbalanced, with the majority of projects falling into the "noRisk" category. To address this, techniques will be employed to mitigate the effects of this imbalance.

The final output will be a classification of new projects (2021–2027), which can then be monitored at early deadlines with clear risk-level exposure. This approach will enable more proactive management and better allocation of public resources.

#### Rationale
The study is critical as it addresses the need to optimize public resource management by identifying projects at risk of failure. This approach enables proactive intervention and better allocation of funds, ultimately ensuring more efficient use of public resources.

#### Research Question
Can we predict the risk level (low, medium, or high) of ongoing publicly funded projects in Italy, based on available project data, to improve public resource management?

#### Data Sources
The primary data source will be OpenCoesione (https://opencoesione.gov.it/it/opendata/#!progetti_section). The dataset for projects spanning 2014–2020 will serve as the training dataset, while projects from 2021–2027 will be used for testing.

I used at the moment:
- [Project portfolio 2014-2020 -- too large not imported](Data_OC/progetti_esteso_2014-2020_20240831.parquet)
- [Project portfolio 2014-2020 -- imported for 2014-2020 FESR - part of the total not imported](Data_OC/df1.parquet)
- [Project portfolio 2021-2027](Data_OC/progetti_esteso_2021-2027_20240831.parquet)
- [Metadata structure of project information](Data_OC/metadati_progetti_tracciato_esteso.parquet)

#### Methodology

Data Preparation and Classification
I performed data cleaning and manual classification on the 2014–2020 dataset. Two new fields were created to aid in classification:

Delay: The duration beyond the planned completion date.
Percentage of Unutilized Funds: The proportion of allocated funds left unused.
Using these fields, projects were classified into four categories:

No Risk (0)
Low Risk (1)
Medium Risk (2)
High Risk (3)

2) To simplify the modeling process, I derived two additional variables:

Project Duration: Total days from start to planned end.
Marginal Cost per Day: Cost divided by project duration.
These variables, along with other selected features available at project inception (e.g., text, numeric, categorical), were used to train predictive models. Several algorithms were applied to identify the best-performing model for risk prediction.

3) The trained model will be applied to the 2021–2027 dataset, processed similarly to the 2014–2020 data.

#### Results
The developed classification model aims to provide early warnings, enabling better management of ongoing and future publicly funded projects. 

However, challenges arose due to the poor quality of the dataset. Several fields contained conflicting or incomplete information. To address this, I excluded certain fields and defined synthetic variables for classification as described in Step 1.

While predictive modeling yielded promising results, the training process was time-intensive, given the selected features

#### Next steps
Data Aggregation
I plan to create aggregated information for certain features, such as categorizing municipalities by population ranges. Starting with fewer features and gradually adding more data will help reduce training times and improve efficiency.

Integration of Procurement Data (in future)
In future work, I intend to incorporate procurement data related to project suppliers, leveraging sources like ANAC (National Anti-Corruption Authority). Combining procurement information with project-level data could help determine whether identified risk factors are also applicable to suppliers. This extension would facilitate comprehensive risk assessments at both the project and supplier levels, further enhancing public resource oversight and management.


#### Outline of project

- [Project Application](Risk_An_v6_2_rid.ipynb)


##### Contact and Further Information
