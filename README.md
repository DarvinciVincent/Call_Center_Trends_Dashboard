# PWC Power BI Virtual work experience- Call Centre Trends
![PwC Power BI Virtual Case Experience (1)](https://user-images.githubusercontent.com/118357991/227764081-750f7560-c9f7-4563-9cb3-74186769cb42.png)

## Table of Contents :

- [Problem Statement](https://github.com/DarvinciVincent/Call_Center_Trends_Dashboard/blob/main/README.md#problem-statement-)
- [Datasource](https://github.com/DarvinciVincent/Call_Center_Trends_Dashboard/blob/main/README.md#datasource-)
- [Data Preparation](https://github.com/DarvinciVincent/Call_Center_Trends_Dashboard/blob/main/README.md#data-preparation)
- [Data Analysis (DAX)](https://github.com/DarvinciVincent/Call_Center_Trends_Dashboard/blob/main/README.md#data-analysis-dax)
- [Insights](https://github.com/DarvinciVincent/Call_Center_Trends_Dashboard/blob/main/README.md#insights-)


## Problem Statement :
In this project Create a dashboard in Power BI for the call center manager that reflects all relevant Key Performance Indicators (KPIs) and metrics in the dataset.

Possible KPIs include (but not limited to):

- Overall customer satisfaction
- Overall calls answered/abandoned
- Calls by time
- Average speed of answer
- Agent’s performance quadrant -> average handle time (talk duration) vs calls answered

## Datasource :

Dataset used for this task was presented by [Pwc](https://www.pwc.ch/en/careers-with-pwc/students/virtual-case-experience.html) and call centre trends dataset:

Dataset: [Call Centre Trends](https://github.com/DarvinciVincent/Call_Center_Trends_Dashboard/blob/main/01%20Call-Center-Dataset.xlsx)

## Data Preparation:

Completed the Data transformation in Power Query and the dataset loaded into Microsoft Power BI Desktop for modeling.

Call Centre Trends dataset is give table named:

- `Call Center trends dataset` which has `10 columns and 5000 rows` of observation

Data Cleaning for the dataset was done in the power query editor as follows:

- Removed Unnecessary columns
- Removed Unnecessary rows
- Each of the columns in the table were validated to have the correct data type

## Data Analysis (DAX):

Measures used in all visualizations are:

- Avg rating = 'AVERAGE(Sheet1[Satisfaction rating])'

- Avg rating star rating = <br>
'VAR __MAX_NUMBER_OF_STARS = 5<br>
VAR __MIN_RATED_VALUE = 0<br>
VAR __MAX_RATED_VALUE = 5<br>
VAR __BASE_VALUE = [Avg rating]<br>
VAR __NORMALIZED_BASE_VALUE =<br>
	MIN(<br>
		MAX(<br>
			DIVIDE(<br>
				__BASE_VALUE - __MIN_RATED_VALUE,<br>
				__MAX_RATED_VALUE - __MIN_RATED_VALUE<br>
			),<br>
			<br>
		<br>
		1<br>
	)<br>
VAR __STAR_RATING = ROUND(__NORMALIZED_BASE_VALUE * __MAX_NUMBER_OF_STARS, 0)<br>
RETURN<br>
	IF(<br>
		NOT ISBLANK(__BASE_VALUE),<br>
		REPT(UNICHAR(9733), __STAR_RATING)<br>
			& REPT(UNICHAR(9734), __MAX_NUMBER_OF_STARS - __STAR_RATING)<br>
	)'

- Call Answered Rate = <br>
'DIVIDE(<br>
    COUNTROWS(FILTER(Sheet1, [Answered (Y/N)] = "Y")),<br>
    COUNTROWS(Sheet1),<br>
    0<br>
)'

- Calls Abandoned Rate = 'SUMX(Sheet1, IF([Answered (Y/N)] = "N", 1, 0)) / COUNTROWS(Sheet1)'

- Resolved Queries w.r.t Call Answer = 'COUNTROWS(FILTER(Sheet1, [Resolved] = "Y" && [Answered (Y/N)] = "Y"))'

- Y_Answer = 'COUNTROWS(FILTER(Sheet1, Sheet1[Answered (Y/N)] = "Y"))'

- Y_Resolved = 'COUNTROWS(FILTER(Sheet1, Sheet1[Resolved] = "Y"))'

- YValuesColumn = 'IF([Answered (Y/N)] = "Y", "Y", BLANK())'


## Insights :

- Most of the satisfaction ratings from each call are 3 and 4.
- The average satisfaction rating has decreased over the span of three months. January brought the highest satisfaction rating and march the lowest.
- The percentage of issue resolved in January was the highest, with a dip in February. It increased again in march.
- The majority of calls come in the morning.
- The average speed of answer by Joe is the highest.
- The call resolution rate of Jim is the highest, even though the average speed of his answers is lower compared to those of Joe, Martha and Dan. The call answered by - him are also higher than the average number of calls answered.
- Becky's speed of answer is the lowest among all, and her rate of calls resolved is higher. She is in the 5th position in the call resolution rate. 
- Martha has the highest  speed of answered in the sec.

---




