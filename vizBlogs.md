# Visualization Blogs
[Home](https://github.com/grntl/dataVisBlog/blob/eb6b53ed750a854b63c563fde42f9b9ebcaddfd0/README.md) | [Short Form Posts](https://github.com/grntl/dataVisBlog/blob/b1541ee35cb8d109bd1438eee7f3d958f1790daa/shortForm.md) | [Final Assignment](https://github.com/grntl/dataVisBlog/blob/9fd117a4d77a7aaa432f277695ff197ed8c54b8a/finalAssign.md)
***
## October 31
I recently made some visualizations using public CTA ridership data provided by the CTA. The dataset tallies the rides counted at every station from 2001 to 2022. 

I made two visualizations: one shows the average rides per month from 2001-2019, and the other shows the average rides per weekday from 2001-2019. I removed the years 2020-2022 from the equation since those years were so abnormal for transit ridership that they would only muddy an insight I could get from looking trying to find general ridership patterns.

To start out, I loaded in the following packages:

```
library(tidyverse)
# install.packages("fauxnaif", dep = T)
# install.packages(c('ggthemes', "fauxnaif", "patchwork"))
library(ggthemes)
library(fauxnaif)
library(patchwork)
library(dplyr) 
install.packages('lubridate')
library(lubridate, warn.conflicts = FALSE)
install.packages('scales')
library(scales)
install.packages('viridis')
library(viridis)
```
Then I loaded in the dataset and removed the years 2020-2022
```
ctaRidership <- read.csv(file = 'C:\\Users\\grant\\Downloads\\CTA_-_Ridership_-__L__Station_Entries_-_Daily_Totals.csv')

# converting the date column into the proper date format. We remove 2020-2022 because the data is so abnormal from COVID that it only muddies the insight we get from seeing monthly ridership trends over the course of a typical year.
ctaRidership$date <- as.Date(ctaRidership$date, format = '%m/%d/%Y')
ctaRidership %>%
  filter(ctaRidership$date < '2020-01-01') -> ctaRidership
```
My first graph looked like this:
![Screenshot_20221104_042309](https://user-images.githubusercontent.com/114178136/199940073-2506c676-3b4b-41bb-af32-1db519ba88aa.png)
My code to produce this graph (with annotations):
```
# grouping the data by months. 
ctaRidership %>%
  group_by(month = lubridate::floor_date(date, "month")) %>%
  filter %>%  summarize(amount = sum(as.numeric(rides), na.rm = T)) -> ridershipByMonth

# turning the mongth column into just the month, and then just numeric format so that the data doesn't retain it's yearly values even if it only shows the month in the data set. That way, each year can stack on top of each other such that any particular month means that month for every year in the dataset.
ridershipByMonth$month <- as.numeric(format(ridershipByMonth$month, format = '%m'))

# Make my error upper and lower bars. 19 is the number of years in the data set.
ridershipByMonth %>%
  group_by(month) %>%
  summarize(meanRiders = mean(amount, na.rm = T),
            seRiders = sd(amount, na.rm = T)/sqrt(19)) %>%
  mutate(upper_bound = meanRiders + (seRiders * 1.96),
         lower_bound = meanRiders - (seRiders * 1.96)) -> ridershipByMonth

# Make my graph
ridershipByMonth %>%
  ggplot(aes(x = month, y = meanRiders)) +
  geom_line() +
  geom_point() +
  geom_errorbar(
    aes(ymin = lower_bound,
        ymax = upper_bound)) +
  xlab('Month') + 
  scale_x_continuous(labels = c('Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'), lim = c(0,13), breaks = c(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12)) +
  ylab('Average Rides') +
  scale_y_continuous(labels=c('12,000,000', '13,000,000', '14,000,000', '15,000,000', '16,000,000', '17,000,000'), lim = c(12000000, 17000000), breaks = c(12000000, 13000000, 14000000, 15000000, 16000000, 17000000)) +
  ggtitle('Average Rides per Month from 2001-2019') -> ridershipMonthLine
```
My second graph looked like this:
![Screenshot_20221104_042712](https://user-images.githubusercontent.com/114178136/199940143-b97d1971-6dc5-4f49-a09d-8cf74dd67b95.png)
The code to produce this graph (with annotations):
```
# Find the total number of weeks that have passed. We need to use this for the standard error calculation.
totalWeeks <- as.numeric(difftime(max(ctaRidership$date), min(ctaRidership$date), units="weeks"))

# Make a new column that just shows the day of the week
ctaRidership$weekday <- format(ctaRidership$date, format = '%a')

# Make error bars
ctaRidership %>%
  # First group by date and sum. Not doing this will result in the mean being calculated from things we don't want, such as the mean rides from different stations on one day, since there are observations from multiple stations for any particular day.
  group_by(date) %>% 
  mutate(dailyRiderTotal = sum(rides, na.rm = T)) %>%
  # Now group by weekday and find the mean rides for a given day of the week
  group_by(weekday) %>%
  summarize(meanRides = mean(dailyRiderTotal, na.rm = T),
            seRides = sd(dailyRiderTotal, na.rm = T)/sqrt(totalWeeks)) %>%
  mutate(upper_bound2 = meanRides + (seRides * 1.96),
         lower_bound2 = meanRides - (seRides * 1.96)) -> ridershipByDay

# Make my graph
ridershipByDay %>%
  ggplot(aes(x = weekday, y = meanRides, group = 1)) +
  geom_line() +
  geom_point() +
  geom_errorbar(
    aes(ymin = lower_bound2,
        ymax = upper_bound2)) +
  scale_x_discrete(lim = c('Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun')) +
  xlab('Days of the Week') +
  scale_y_continuous(labels = c('200,000', '300,000', '400,000', '500,000', '600,000'), lim = c(200000, 600000), breaks = c(200000, 300000, 400000, 500000, 600000)) +
  ylab('Average Rides') +
  ggtitle('Average Rides per Weekday from 2001-2019') -> ridershipWeekday
```
### A visualization I found recently that I disliked
I found this in a tweet from Fortune magazine.

![Ff2PBHCWYAEVEy5](https://user-images.githubusercontent.com/114178136/199940413-a29a95df-661a-4028-9ea5-e720517f8787.png)

The part that really doomed this visualization is the legend. First of all, what is a Zillow Home Value Index? I have no clue what any numbers on the color scale mean. Additionally, the x axis of the color scale itself is not even. The left end of the color scale is -10, but the middle is 0, and then the right is 50. I would just put some plain old percentage values on the scale, instead of whatever the Zillow  Home Value Index is.

## October 10
### A visualization I found recently that I disliked
I found this data visualization on from a [Wall Street Journal article about carbon emissions](http://graphics.wsj.com/climate-talks/). 
![Web capture_10-10-2022_04257_graphics wsj com](https://user-images.githubusercontent.com/114178136/194805121-7aff6336-04ab-4de9-8db5-ec44181f2801.jpeg)

I dislike this visualization because for a rather simple reason. I understand that the countries are in order of largest to smallest carbon emitters, but the groupings make it seem as if the EU and India had something in common other than that, and especially for the last group. There's no way they couldn't have done this without grouping them in that way. Also, I'm fairly confused at how they are ordered the way they are when Indonesia's units are lower than some below it in the rankings. It is cool to put the visualization in the shape of the countries, but I would have preferred the squares just be stacked up in nice bars in order of largest emitters to smallest. It's simpler and easier to understand. 
### A visualization I found that I liked
![Web capture_10-10-2022_222639_archive ph](https://user-images.githubusercontent.com/114178136/194990371-747ee777-205c-4425-a8f1-ac75da6bba2a.jpeg)

I found this from a [New York Times article about abortion costs](https://archive.ph/NKrTS). I liked this visualization because it kept the y axis consistent throughout every single graph despite the fact that there were many of them and that one even went off the chart. In my opinion, that's preferable to having a different y-axis for every single graph because then it would be hard to evaluate or compare across graphs. 

A bit of code that might produce the same thing with two graphs would be:
EDIT: I now know that this could be done quite nicely with a facet wrap.
```
clinic1Graph %>%
  ggplot(aes(x = year) + 
  geom_line(aes(y = abortionClinic1)) +
  ylim(0, 1000)
  
clinic2Graph %>%
  ggplot(aes(x = year) +
  geom_line(aes(y = abortionClinic2)) + 
  ylim(0, 1000)
```
This way, there are two graphs. I got the idea for this code from [stackOverflow](https://stackoverflow.com/questions/30375600/how-to-plot-multiple-lines-for-each-column-of-a-data-matrix-against-one-column), because I realized that the table for this data would have to be structured kind of oddly. The left hand column would be a sort of index by year, and the columns would be each abortion clinic, with the values being the prices. I'd obviously have to be selective about the years by picking specifically the 2021-2022 row, but I'm not sure how to do that yet.
### My own data visualization
I found a dataset that was put on tidytuesdays on GitHub in 2021 about [transit costs](https://github.com/rfordatascience/tidytuesday/blob/master/data/2021/2021-01-05/readme.md). I'm very into transit, and it's a huge problem in America that transit costs an insane amount to build—it means we end up with some of the worst public transit in the world, or none at all.

First, I did ```head(transit_cost)``` in order to see what the table looked like. I could see that it had various cities as rows, with their country as a variable, along with the cost per kilometer.

Then I cleaned the data by removing NAs. 

```
transitCleaned <- na.omit(transit_cost)
```
In order to do the country-by-country analysis I wanted to do, I needed to find out what countries there were in the database. I used the code below to find all the unique values in the 'country' column of the datatable and also put them into a vector that I could utilize later.
```
countries <- c(unique(transitCleaned$country))
countries
```
Then I made a function where if I gave it a country, it would go and find the average value of the cost per kilometer from that country by finding all the entries in the database from that country and averaging their values in the cost per kilometer column.
```
countryAvg <- function(x) {
  tally <- 0
  totalCost <- 0
  for (i in 1:nrow(transitCleaned)) {
    if (transitCleaned$country[i] == x){
      totalCost <- totalCost + as.numeric(transitCleaned$cost_km_millions[i])
      tally <- tally + 1
    }
  }
  return(totalCost / tally)
}
```

I made an empty vector that I would fill with the averages for every country. I used a for loop to iterate through the vector of countries I had made earlier and call on the function for every one of the countries. Each iteration appends the average cost per kilometer of that country onto the empty vector so that by the time the for loop as gone through every country, the vector should now be filled with the average cost per kilometer for every country.
```
averages <- c()
for (c in countries) {
  averages <- append(averages, countryAvg(c))
}
averages
```
I combined the countries vector and the averages together into one new dataframe that I would work with.
```
avgCostCountry <- data.frame(countries, averages)
avgCostCountry
```
Then I made a bar graph with the data.
```{r}
avgCostCountry %>%
  ggplot(aes(x = as.factor(countries), y = averages)) +
  theme(axis.text.x = element_text(angle = 90, hjust = 1)) +
  geom_col(stat = 'identity') +
  labs(x = "Country", y = "Average Real Cost in Millions of USD")
``` 
Unfortunately, I cannot understand for the life of me how to shift the axis so that the country labels are actually aligned with their bars. But if you inspect closely, you can see how the column for US is just far beyond any other country. 
![avgCostCountry](https://user-images.githubusercontent.com/114178136/195026606-4e4dff42-1cf3-404e-af6f-be0e6870e9e1.png)
