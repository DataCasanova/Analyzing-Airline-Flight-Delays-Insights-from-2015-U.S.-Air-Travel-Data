# Analyzing-Airline-Flight-Delays-Insights-from-2015-U.S.-Air-Travel-Data
This analysis aims to understand flight volume trends, assess departure delays, and evaluate airline reliability to optimize scheduling and improve passenger satisfaction. By examining delay patterns and cancellation causes, we seek to enhance operational efficiency and provide valuable insights for travelers and airlines.

# Project Overview
## Objective:
**As a data analyst hired by Conpass .co, I was tasked with analyzing the dataset of over 5,000,000 commercial airline flights in 2015.** **The goal is to identify patterns in flight delays, cancellations, and airline reliability to provide insights and recommendations that will benefit the airline industry economically.**

## Analysis Goals:
- How does the overall flight volume vary by month? By day of the week?
- What percentage of flights experienced a departure delay in 2015? Among those flights, what was the average delay time, in minutes?
- How does the percentage of delayed flights vary throughout the year? What about for flights leaving from Boston (BOS) specifically?
- How many flights were canceled in 2015? What percentage of cancellations were due to weather? What percentage were due to the airline/carrier?
- Which airlines seem to be most and least reliable, in terms of on-time departure?


## Approach to the Challenge
### Data Exploration and Analysis:
•	Import and explore the dataset to understand its structure and contents.
•	Perform data cleaning and transformations as needed.
•	Conduct specific analyses to answer the recommended questions.
•	Summarizing Insights:


Import and explore the dataset to understand its structure and contents.
Perform data cleaning and transformations as needed.
Initial Data Exploration:
Import and explore the dataset to identify key columns: airline name, flight number, origin/destination airport, flight distance, scheduled/actual departure and arrival times.
Replaced Value

Handle missing values and correct any inconsistencies in the data.

•	Table.ReplaceValue(#"Filtered Rows","","E”, Replacer.ReplaceValue, {"CANCELLATION_REASON"}),
•	Table.ReplaceValue(#"RemovedColumns”, null,0, Replacer.ReplaceValue, {"ARRIVAL_TIME"}),
•	Table.ReplaceValue(#"ReplacedValue1”, null,0, Replacer.ReplaceValue, {"ARRIVAL_DELAY"}),
•	Table.ReplaceValue(#"Replaced Value2”, null,0, Replacer.ReplaceValue, {"TAXI_IN"}),
•	Table.ReplaceValue(#"Filtered Rows1”, null,0, Replacer.ReplaceValue, {"WHEELS_ON"}),
•	Table.ReplaceValue(#"Replaced Value4”, null,0, Replacer.ReplaceValue, {"AIR_TIME"}),
•	Table.ReplaceValue(#"Replaced Value5”, null,0, Replacer.ReplaceValue, {"WHEELS_OFF"}),
•	Table.ReplaceValue(#"Replaced Value6”, null,0,Replacer.ReplaceValue,{"ELAPSED_TIME"}),
•	Table.ReplaceValue(#"Filtered Rows2",null,0,Replacer.ReplaceValue,{"DEPARTURE_DELAY"}),
Add Column
Create new columns for delay calculations, day of the week, and month.
•	Table.AddColumn(#"Replaced Value7", "Name of Day", each if [DAY_OF_WEEK] = 1 then "Sun" else if [DAY_OF_WEEK] = 2 then "Mon" else if [DAY_OF_WEEK] = 3 then "Tue" else if [DAY_OF_WEEK] = 4 then "Wed" else if [DAY_OF_WEEK] = 5 then "Thur" else if [DAY_OF_WEEK] = 6 then "Fri" else if [DAY_OF_WEEK] = 7 then "Sat" else null),
•	Table.AddColumn(#"Replaced Value14", "Month Name", each if [MONTH] = 1 then "Jan" else if [MONTH] = 2 then "Feb" else if [MONTH] = 3 then "Mar" else if [MONTH] = 4 then "Apri" else if [MONTH] = 5 then "May" else if [MONTH] = 6 then "Jun" else if [MONTH] = 7 then "Jul" else if [MONTH] = 8 then "Aug" else if [MONTH] = 9 then "Sep" else if [MONTH] = 10 then "Oct" else if [MONTH] = 11 then "Nov" else if [MONTH] = 12 then "Dec" else null),
Transform date and time columns to appropriate formats for analysis
•	Table.SelectRows(#"Changed Type1", each ([DEPARTURE_DELAY] = -18 or [DEPARTURE_DELAY] = -16 or [DEPARTURE_DELAY] = -15 or [DEPARTURE_DELAY] = -14 or [DEPARTURE_DELAY] = -13 or [DEPARTURE_DELAY] = -12 or [DEPARTURE_DELAY] = -11 or [DEPARTURE_DELAY] = -10 or [DEPARTURE_DELAY] = -9 or [DEPARTURE_DELAY] = -8 or [DEPARTURE_DELAY] = -7 or [DEPARTURE_DELAY] = -6 or [DEPARTURE_DELAY] = -5 or [DEPARTURE_DELAY] = -4 or [DEPARTURE_DELAY] = -3 or [DEPARTURE_DELAY] = -2 or [DEPARTURE_DELAY] = -1 or [DEPARTURE_DELAY] = 0))


Cleaning Data
Power Quary

Conduct specific analyses to answer the recommended questions.
Analysis and Findings
1. Overall Flight Volume by Month and Day of Week
Monthly Flight Volume: Analyze the total number of flights each month to identify seasonal trends.
Day of Week Flight Volume: Analyze the total number of flights each day of the week to understand weekly patterns.
Findings:
Monthly Volume: Flight volume tends to be higher in the summer months (May Jun and July) and lower in the winter months (January, February) follow by a decline in Sept and Nov.
Day of Week Volume: Flight volume is generally consistent throughout the week, with a slight increase on Wednesday and Sundays.

2. Percentage of Flights with Departure Delays and Average Delay Time
To get the total number of Delay departure we need to categories the Departure delay time into Early, delay and Same Time
 Departure Category = 
    			'YourTable'[Departure delay] < 0, "Early",
   	 		'YourTable'[Departure delay] = 0, "Same Time",
  			 'YourTable'[Departure delay] > 0, "Delay"

Percentage of Delayed Flights: Calculate the proportion of flights that experienced a departure delay.
Average Delay Time for delayed flights is 4.84%
Findings:
Percentage Delayed: Approximately 57.2% of flights experienced a departure delay in 2015.




3. Variation of Delayed Flights Throughout the Year and for Boston (BOS)
Yearly Variation: Analyze how the percentage of delayed flights changes month by month.
Boston-Specific Delays: Focus on flights departing from Boston (BOS) to see if there are any notable differences.
Findings:
Boston Delays: Flights from Boston (BOS) show a similar pattern but with a slightly higher percentage of delays in the May, Sept and Nov months compared to the overall Month.
4. Flight Cancellations and Reasons
Total Cancellations: Count the total number of flight cancellations in 2015.
Cancellation Reasons: Determine the percentage of cancellations due to weather and airline/carrier issues.
Findings:
Total Cancellations: There were 90k flight cancellations in 2015.
Cancellation Reasons: Approximately 54.35% of cancellations were due to weather, while 45.63% were attributed to airline/carrier issues, National Air System and Security

5. Airline Reliability in Terms of On-Time Departure
When selecting the most and least reliable airlines in terms of on-time departures, consider the on-time departure rate, the total number of flights operated, and the consistency of performance across different time periods.
Calculation use in getting the departure rate
DelayedDepartureRate = 
VAR TotalFlights = COUNTROWS(Flights)
VAR Delayed Flights = COUNTROWS (FILTER (Flights, Flights [DepartureCategory] = "Delay"))
RETURN
DIVIDE (DelayedFlights, TotalFlights, 0)
OverallDepartureRate = 
VAR TotalFlights = COUNTROWS(Flights)
VAR OnTimeOrEarlyFlights = COUNTROWS (FILTER (Flights, Flights [DepartureCategory] IN {"Early", "Same Time"}))
RETURN
DIVIDE (OnTimeOrEarlyFlights, TotalFlights, 0)
Most Reliable: Airline UA WN and Airline NK had the highest on-time departure rates, with over 50% of their flights departing on time.
Least Reliable: Airline HA and Airline AS had the lowest on-time departure rates, with less than 30% of their flights departing on time.

Recommendations with Relatable Examples
Targeted Strategies for Busy Periods:
Example: Just like a retail store hires extra staff during the holiday shopping season, airlines could increase crew availability and streamline operations during October, November and May where there is high rate of delay in a months and busy travel days like Wednesday.
Delay Mitigation:
Example: Similar to how a city might deploy more snowplows during a forecasted storm, airlines could improve winter preparedness by investing in de-icing equipment and improving weather prediction capabilities.
Improve Reliability:
Example: Imagine if your unreliable friend started using a calendar app to keep track of appointments. Airlines can use better scheduling software and allocate resources more efficiently to ensure timely departures.
Cancellation Policies:
Example: Like how a restaurant might offer free appetizers to diners affected by a long wait time, airlines could improve their customer service and contingency plans to better handle weather-related disruptions and reduce the impact on passengers.
Customer Communication:
Example: Think about how much more reassured you feel when a restaurant keeps you updated on your table's status during a wait. Similarly, airlines can enhance communication with passengers about delays and cancellations through timely updates and clear information, improving overall satisfaction.
By using these relatable examples, the findings and recommendations become easier to understand and apply to real-world scenarios 














Import and Explore the Dataset:

Understand its structure and contents.
Identify key columns: airline name, flight number, origin/destination airport, flight distance, scheduled/actual departure, and arrival times.
