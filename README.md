# NYC YELLOW TAXI RIDERS ARE STILL PRETTY GOOD TIPPERS
This project set out to analyze the tens of millions of taxi trip records published by the [NYC Taxi and Limousine Commission](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page) between January 2019 and April 2023. I wanted to to see how tipping patterns have changed over the years, with the hypothesis that cab riders are tipping less due to an increasing inflation rate and cost of living. The findings, however, were pretty anticlimactic: the change in median tip percentage of total fare over the years is marginal. I was, however, surprised to learn that the average tip has hovered around 26% of the total taxi fare since 2019.

## Data Collection
<p> The NYC Taxi and Limousine Commission (TLC) publishes separate monthly Parquets of trip record data for Yellow Taxis, Green Taxis (boro taxis), For-Hire Vehicles and High Volume For-Hire Vehicles, such as luxury limos, Uber, Lyft, etc. </p>

For this project I chose to focus on Yellow Taxi data from January 2019 to April 2023 (the most recently available data), which includes information such as pick up/drop off location, trip distance, fare price, etc. Find the full data dictionary [HERE](https://www.nyc.gov/assets/tlc/downloads/pdf/data_dictionary_trip_records_yellow.pdf)

<p> I went back to 2019 to included data from pre-covid times to see whether the pandemic had any substantial influence (spoiler alert: it did). </p>

The data is quite large, so I linked to the parquets from the NYC Open Data [website](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page) to create multiple DataFrames in a Jupyter Notebook [nyc_yellowtaxi.ipynb](https://github.com/karinashed/nyc_yellow_taxi_rides/blob/main/notebooks/nyc_yellowtaxi.ipynb), which also contains most of the code used to analyze the data. I had to make a separate notebook for the 2019 data [nyc_yellowtaxi_2019.ipynb](https://github.com/karinashed/nyc_yellow_taxi_rides/blob/main/notebooks/nyc_yellowtaxi_2019.ipynb) to prevent the kernel from crashing. The third notebook [nyc_yellowtaxi_to_visualize.ipynb](https://github.com/karinashed/nyc_yellow_taxi_rides/blob/main/notebooks/nyc_yellowtaxi_to_visualize.ipynb) was used to combine all of the data from 2019 through 2023 and export it into csv format for visualization. All csvs are in the folder titled `csvs`.

#### The analysis looks at three separate trends:
- What percent of the total fare riders have tipped over time (looked at the median percentage for each month to exclude any crazy outliers)
- The overall number of taxi rides 
- The payment method used to pay for rides (cash vs. credit card)

<p> The steps I took to analyze the data are detailed in each of the notebooks.</p>

### Note on Cleaning:
The Parquets were clearly meant to show rides for a specific month and year, but each had a small number of outlier dates (that ranged from 2002-2080). The erroneous future dates led me to completely omit all outlier dates from each respective DataFrame,  even if the date was relevant to the larger analysis (e.g., 2020 ride data that showed up in 2023 parquets). I also omitted all trips that had both a distance or trip fare listed as less than or equal to zero. I owe the TLC a call to figure out why there are crazy dates and negative fare amounts included in the data. 

### Lessons Learned:
Since I had to make so many separate DataFrames, I spent a lot of time trying to keep my notebooks organized and thinking through which part of the data I needed to pull to answer each question I was looking at. For instance, for ride count I needed to look at all of the data regardless of payment type (other categories include “no charge” and “dispute”), but to analyze median tip I could only look at trips that passengers paid for with credit card. There were quite a few moments where I’d do an analysis, realize I wasn’t looking at the right subset of the data, and have to stop, think and redo. 

### Regrets:
If I had more time I would have compared the Yellow Taxi Data with the High Volume For-Hire Vehicles Data (Uber, Lyft, etc.). I started and tried to make a dataframe out of the 2019 parquets, but gave up when it wouldn’t complete after 15 minutes. I imagine each parquet is massive. I also had the idea to map information on pick up and/or drop off location (such as, a map of median tip by pick up location), but the .geojson zone map was too large to upload to DataWrapper, and I didn’t have the time to figure out how to do it with Flourish. The TL/DR is there’s a lot more I wanted to do with this data and I have *a lot* more to learn in order to do so. 

Find the published project [here](https://karinashed.github.io/nyc-yellow-taxi-rides/)
