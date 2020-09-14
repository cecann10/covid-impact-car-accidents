
# COVID-19's Effect On Car Accidents
A Student Project for Metis Data Science Bootcamp Summer 2020.

## GENERAL INFORMATION
Author & Investigator: **[Celina Plaza](https://github.com/cecann10)**

Institution: **Metis**

Email: celina.plaza@gmail.com

Date of data collection: 2020-08-26 through 2020-08-29

## PROJECT OVERVIEW
### Context
On average, the United States has ~36k fatalities per year from vehicle accidents.   There are behavioral actions that are associated with accidents -- e.g. not wearing a seatbelt, speeding, texting, etc -- but there are also external factors, such as weather, temperature, geography, whether at an intersection, that can play a part in propensity for an accident to occur.

With the spread of COVID and cities and states ‘locking down’ across the country, this brings in a new external factor to consider.  While COVID has had countless negative effects on the world, but during the height of stay-at-home orders by states there were reports of less cars on the road leading to cleaner air, clearer views, and more recreation; glimmers of unintended positive impacts.  Could COVID also be associated with fewer and/or less severe accidents?  This project explored that question.



### Goal

Using classification modeling techniques, identify what ‘evergreen’ external factors (geography, weather conditions, traffic signals in the area, etc.) have a relationship with the level of severity of an accident and also examine whether the ‘new’ external factor of the COVID-related lockdown rules slowed traffic in states has a relationship with the severity of an accident.

Conduct additonal analysis to determine if COVID-related lockdown rules reduced frequency of accidents in general, looking state by state since periods of stay-home varied across the nation.

### Approach
To reach this project’s goals, traffic data on car accidents from February 2016 to June 2020 across the US (~3.5M accidents) was collected and combined data on when states (if ever) implemented ‘stay-at-home’ orders for citizens and then also when they (if yet) reopened the state.

Then 20 states with the most car accidents (=86% of total car accidents in US) were examined for changes in severity or frequency by comparing each states unique stay-home period with equivalent periods in 2017-2019.

To get an understanding of the *degree* of impact the stay-home period had on severity of car accidents in 2020, classification modeling was used by combining 26 'evergreen' variables -- such as weather condition, road signs' presence, time of day -- and added whether stay-home period was in place during time of accident to see if the stay-home variable affected the model, and if so, in a Logistic Regression model which 'direction' it pulled the model by its coefficient either being positive (more severe accident) or negative (less severe car accident).

Severity of a car accident was ranked in four categories:
- Low
- Medium Low
- Medium High
- High


### Findings

**Classification Modeling:**

Multiple featues were considered for the classifcation modeling:
- Whether in a stay-home period
- Temperature (F)
- Humidity(%)
- Visibility(mi)
- Wind Direction
- Wind Speed
- Weather Condition (e.g. Foggy, Snow, Cloudy)
- Presence of traffic signs/guides (e.g. Traffic Signal, Roundabout, No Exit)
- Time of Day (Day or Night)

The Logistic Regression model focusing on 2020 car accidents with 71.6% accuracy was selected and found that the stay-home period did improve the model's accuracy slightly (0.002) towards the direction of the car accident being less severe.

*Variables leaning towards predicting less severe car accidents:*
- Weather Conditions:
  - Clear/Fair
  - Foggy/Hazy
- Signal Presence:
  - Traffic Light
- Intersection Type:
  - Crossing
- **Under 'Stay-Home' Orders**

*Variables leaning towards predicting more severe car accidents:*
- Weather Conditions:
  - Rain/Thunderstorm
  - Snow/Hail
- Time of Day:
  - Nighttime
- Intersection Type:
  - Junction
- Higher Temperature Outside

-----
**States'Severity and Frequency Analysis:**

When examining the top 20 states with most accidents together, it found a:
- 8,870% ‘Low Severity’ increase in 2020 stay-home period compared to average 2017 – 2019 equivalent periods
- 52% increase in car accidents during 2020 stay-home period compared to average 2017 – 2019 equivalent periods

When examining individual states, while in the majority of states trend with the average low severity of car accidents and higher frequency of car accidents, there was great variation between states in the *degree* of that change -- or in a few cases, an opposite direction.  For example, California had a car accident frequency *increase* of 76% during the stay-home 2020 period vs. its 2017-2019 average, while Texas had a *decrease* of 37%.



### Conclusion
The findings of this project indicate that during the stay-home period in the US, there was an increase of frequency of car accidents and a decrease of severity of car accidents, even when accounting for other ‘evergreen’ variables, such as weather and time of day.  Additionally, individual states can vary significantly in degree shifts in frequency and severity.



## METHODOLOGICAL INFORMATION

#### Methods used for collection/generation of data:
- **Car Accident Data**: Car accident data was collected from [Kaggle.com]('https://www.kaggle.com/sobhanmoosavi/us-accidents') and downloaded in a csv format.
- **Stay-At-Home Data by State**: Data regarding when states were in a period of 'stay-at-home' orders was collected by mainly by referencing and cross-referencing [The National Academy for State Health Policy's website]('https://www.nashp.org/governors-prioritize-health-for-all/') and [Littler's website]('https://www.littler.com/publication-press/publication/stay-top-stay-home-list-statewide').  At times 3rd and 4th sources were used to verify a date listed or to find an updated date since stay-at-home orders were shifting often and after some of the main data sources had been published.  A master list of dates for each state was then created and combined with the car accident data based on what state the car accident was listed in.



#### Methods for processing and cleaning the data:
Original data was narrowed to only the variables that were needed for the modeling and/or analysis of COVID's effects.  Samples with null values were removed.

Weather Conditions were bucketed so that over 100 unique values were reduced to 8:
1. Rain/Thunderstorms
2. Snow/Hail
3. Cloudy
4. Foggy/Hazy
5. Dusty
6. Clear/Fair
7. Smoke
8. Wintry Mix


For the classificaion modeling, the target variable, Severity of Car Accident, originally had 4 values (1,2,3,4) that ranked sevrity of the accident.  The 1 and 4 ratings were too minor to use in modeling (1 was below 0.05% and 4 was below 0.3%), so only the 2 and 3 ratings were used in modeling -- therefore the model was a binary classificaion model (2 being majority class and 3 being minority class).


#### Methods for analysis and modeling:
For classification modeling, Logistic Regression, XGBoost, and Random Forest models were all tested and compared.

'Dummies' were created for categorical data were needed and data was scaled for Logistic Regression modeling.  Common methods were used for address imbalance of the classes (undersampling, ADASYN), but utlimately did not improve the model and were therefore not used.


## DATA & FILE OVERVIEW
*Note all notebooks were originally run and developed from Google Cloud Platform*

- **File List**:
    * [Data Collection & EDA](modeling_and_analysis/car_accidents_eda.ipynb) - worksheet for pulling in all car accident and stay-at-home by state data.  Then data was combined to master document, filtered to key features, and cleaned.

    * [Model Development](modeling_and_analysis/car_accidents_model.ipynb) - worksheet where car accident severity classification models were explored, developed, analyzed, and refined.

    * [Analysis](modeling_and_analysis/accident_covid_analysis.ipynb) - worksheet where car accident severity and frequency was analyzed for the top 20 states with the most car accidents (representing 86% of total US car accidents)

    * [CSVs](modeling_and_analysis/csv) - the originl csv used for collection of raw data on car accidents

- **Relationship between files**:
    * Files listed above are in order of collection and build from each other.  Pickles were removed from the folders due to file-size restrictions, but if notebooks are run, pickles will appear and then each notebook will be able to run independent of the other.

- **Presentation Deck**:
    * [PDF version](presentation/COVID_Car_Accidents_Presentation.pdf)
    * [PPT version](presentation/COVID_Car_Accidents_Presentation.pptx.zip)

## SHARING/ACCESS INFORMATION

 - Licenses/restrictions placed on the data: This car accident dataset has been distributed only for Research purposes, under Creative Commons Attribution-Noncommercial-ShareAlike license (CC BY-NC-SA 4.0). You are not allowed to directly download data from this file; go to [Kaggle.com]('https://www.kaggle.com/sobhanmoosavi/us-accidents') to collect data and follow their usage guidelines.

 - **Recommended citation for this dataset:**
- Car Accident data:
    - Moosavi, Sobhan, Mohammad Hossein Samavatian, Srinivasan Parthasarathy, and Rajiv Ramnath. “A Countrywide Traffic Accident Dataset.”, 2019.
    -   Moosavi, Sobhan, Mohammad Hossein Samavatian, Srinivasan Parthasarathy, Radu Teodorescu, and Rajiv Ramnath. "Accident Risk Prediction based on Heterogeneous Sparse Data: New Dataset and Insights." In proceedings of the 27th ACM SIGSPATIAL International Conference on Advances in Geographic Information Systems, ACM, 2019.

  - Stay-At-Home by State data:
    - [The National Academy for State Health Policy's "Chart: Each State’s COVID-19 Reopening and Reclosing Plans and Mask Requirements" August 20, 2020]('https://www.nashp.org/governors-prioritize-health-for-all/')
    - [Littler's "Stay on Top of 'Stay At Home' – A List of Statewide Orders" May 20, 2020]('https://www.littler.com/publication-press/publication/stay-top-stay-home-list-statewide')


## Technologies/Packages Used
  * Google Cloud Platform
  * Jupyter Notebook
  * Python
  * pandas
  * numpy
  * imblearn
  * pickle
  * statsmodels
  * seaborn
  * sklearn
  * matplotlib
  * yellowbrick
  * mlxtend


## Presentation Materials Used
  * Slidesgo - Template
  * freepik - Photos
  * mapchart.net - US Maps
