# Short Form Posts
[Home](https://github.com/grntl/dataVisBlog/blob/a6217a8dae80b358d75b71554485020a7e35e4e7/README.md) | [Visualization Blogs](https://github.com/grntl/dataVisBlog/blob/05aa0aa680d6fafe407189b80aa74af30f474d7d/vizBlogs.md) | [Final Assignment](https://github.com/grntl/dataVisBlog/blob/9fd117a4d77a7aaa432f277695ff197ed8c54b8a/finalAssign.md)
***
## Visualizing Civil Society and Freedom of Expression (short form blog \#2)

We are interested broadly in how civil society and government censorship efforts are related, interact, and change over time and region. The data we use to explore these two factors is from the [VDEM](https://www.v-dem.net/) measuring various aspects of democracy. 

Civil society and government censorship efforts are very important to political society. Civil society is defined the space between the state and private life where people form communities and groups to pursue their interests, like unions, religious groups, interest groups, and so on. Government censorship efforts is the degree to which the government tries to censor print or broadcast media. These variables differ in that a society can still have civil society where people meet and advocate their interests to those in power through direct contact, and yet government censorship will not affect civil society unless groups try to broadcast put their interests into some form of media. Nevertheless, the latter scenario does often happen, so we would like to use visual analysis of the data to observe their relationship.

![Screenshot_20221116_090718](https://user-images.githubusercontent.com/114178136/202345988-d7affaf8-96af-42ab-b265-5890a19a00a7.png)
![Screenshot_20221116_090653](https://user-images.githubusercontent.com/114178136/202345998-838daa14-a603-48d9-a345-a2a258674139.png)
![Screenshot_20221116_090554](https://user-images.githubusercontent.com/114178136/202346006-7699e457-10ea-4b7c-b7d2-8a7c2333fbfd.png)
![Screenshot_20221116_090522](https://user-images.githubusercontent.com/114178136/202346025-2a0330af-6d7f-463d-bb83-2a97e322b17e.png)

## Visualizing CTA Ridership (short form blog \#1)

Public transit is a cornerstone of urban communities. It allows residents of a city to commute to work without having to be in a car on the street. This is important for many reasons. First, the environmental benefits of having less car trips is huge. Not only is it better for the climate, but it makes for a better city in terms of noise, pollution, and safety. Second, public transit allows many people to save money on transit because they do not have to buy a car. 

Much of the conversation around public transit surrounds its ridership. The ridership is often used to justify funding or building transit in the first place. It becomes a contentious topic among both politicians and stakeholders, with those who are wary of giving more funding to public transit pointing to low ridership and such. While this potentially gets the causation backwards, as increased ridership is often driven by a well-funded, effective public transit system, ridership might still persist in high numbers despite a poorly funded public transit system. In that case, the case is even stronger for better public transit funding. 

Recently, ridership come under scrutiny, not only because the adoption of public transit is increasingly considered a key part of a possible solution to climate change, but also because the COVID-19 pandemic reduced ridership immensely, while the fixed costs of system maintenance was still being paid out from city budgets. [As evidence for this, the federal government helped to fund public transit systems that were experiencing revenue gaps](https://www.transit.dot.gov/coronavirus). 
To investigate this issue, I used the official [CTA dataset “CTA – Ridership – ‘L’ Station Entries – Daily Totals"](https://data.cityofchicago.org/Transportation/CTA-Ridership-L-Station-Entries-Daily-Totals/5neh-572f). The dataset consists of five columns: the station ID, the station name, date, the type of day (weekday, Saturday, Sunday/holiday), and also the number of rides. This data is fairly reputable because it is collected by the official agency itself. The data goes from the beginning of 2001 up through July, 2022. 
I want to use this data to visualize and understand how ridership has historically been on the CTA, and how it has looked in recent years. To begin, I made a bar plot of the ridership total for each year. 

![This is a bar plot graph showing ridership by year](https://user-images.githubusercontent.com/114178136/197940422-06c31da6-3350-478c-a079-215a0ace58a4.png)

This aggregates data from every single station for every single day of that year and adds them together. After making this graph, it is very clear just how much COVID-19 affected ridership. However, it has also been increasing since 2020, as the data for 2022 only goes through July, yet the ridership is about three-quarters of the way to 2021’s ridership total. 

We can look at this in more detail by looking at monthly ridership over the same time period. 

![This is a line graph showing ridership by month, from 2001 to 2022](https://user-images.githubusercontent.com/114178136/197941144-c198938f-0d8a-4186-9e1a-3aa6da187cd4.png)

Here, you can see how ridership fluctuates each year, such as how ridership tends to decrease in the winter. Because the first graph is cumulative, it does not show just how fast the monthly ridership totals have begun to rebound, since a cumulative tally at the end of a year takes time to reflect what has happened over the course of the year. You can also see the precipitous fall after COVID-19 began. More importantly, this graph allows us to see just how fast the recovery is happening. The seasonal dip from the winter of 2021 into 2022 finished much higher than recent lows, giving a decent ridership base to climb from through the rest of 2022. 

One thing to note from both the first and second graph is that they show a ridership peak around 2015, from which ridership subsequently began a slow decline up to the pandemic. This raises an interesting question that goes unanswered in this data visualization, and for which this dataset, or any dataset, is unsuitable to answer: will a pandemic rebound buck the steady pre-pandemic decrease in ridership, or will it return to where we might have expected ridership to have made a steady decrease to had the pandemic not occurred? Or, ridership could obviously also never rebound to either of those two levels. 

Next, I’m curious about how fast the ridership total tends to increase over the course of the year. That means that for each year, I want a line which at any given month of the x axis shows the running total of ridership up to that point since the start of the year:

![This is a line graph with a line for each year showing the cumulative total ridership over the course of a year](https://user-images.githubusercontent.com/114178136/197940555-cb73c1bf-10ab-4e57-8395-1b6fa40c10af.png)

I was unable to add a legend due to the way I had to program it (likely suboptimal), but to explain the coloring, all the black lines are from 2001-2019. The yellow line is 2020. It was going on the same general trajectory as all the previous years, but plateaus right when COVID-19 hit. 2021 is in blue. The trajectory of the 2021 total ridership over the year steadily increases, but its rate of increase is much lower than those of previous years (excluding 2020, of course). Finally, the red line is 2022. Although the red line started the year out with similarly low ridership as the winter of 2021, it is climbing a little faster than in 2021, meaning that more people are coming back to use public transit again. Perhaps something we might see in the near future is the line for each particular year steadily climbing up to where the black lines from pre-COVID ridership years are clustered.

![This is a line graph with a line for each year showing the ridership per month over the course of a year](https://user-images.githubusercontent.com/114178136/197940574-ece0f198-18a6-461e-bcb8-df7f9427e7c4.png)

This graph also shows ridership over the course of each year, but rather than showing cumulative counts, it shows the riders each month. The outlook from this graph might make a hope for a speedy public transit ridership recovery doubtful. The red line showing ridership each month for 2022 seems to be flattening out compared to the same line in 2021. When viewed against the pre-COVID lines, this is somewhat typical when only observing the trajectory of the graph, while ignoring the magnitude, as the pre-Covid years seemed to have pretty flat lines as well. However, there is clearly no guaranteed inexorable climb in the recovery, and officials will have to work to encourage the public to utilize public transit again, rather than relying on some sort of natural recovery.

The data visualization did not really find anything particularly new. The conclusions made here by looking at the data visualizations are corroborated by news articles that are already on the Internet. Nevertheless, it helps us visualize in a few ways a lot of the trends that news articles have only described in words. For example, the first article that talks about recent ridership after a simple "CTA ridership” Google search is one by [Streetsblog Chicago](https://chi.streetsblog.org/2022/09/26/some-good-news-about-cta-for-a-change-ridership-has-reached-a-new-pandemic-era-record/), which has data visuals other than a picture of a table. I did not find anything better from all the links of the first page of Google results for that search. So while these graphs do not discover anything new, the media out there for the public to consume very much utilize these sort of graphics, or similar and better ones, so that readers do not have to try and picture what a certain percentage increase or decrease might look like.

Citations:

[Chicago Data Portal for the dataset CTA - Ridership - 'L' Station Entries - Daily Totals: https://data.cityofchicago.org/Transportation/CTA-Ridership-L-Station-Entries-Daily-Totals/5neh-572f](https://data.cityofchicago.org/Transportation/CTA-Ridership-L-Station-Entries-Daily-Totals/5neh-572f)

Packages used in the data visualization:
- [tidyverse](https://www.tidyverse.org/)
- [ggthemes](https://yutannihilation.github.io/allYourFigureAreBelongToUs/ggthemes/)
- [fauxnaif](https://cran.r-project.org/web/packages/fauxnaif/index.html)
- [patchwork](https://cran.r-project.org/web/packages/fauxnaif/index.html)
- [dplyr](https://dplyr.tidyverse.org/)
- [lubridate](https://lubridate.tidyverse.org/)
- [scales](https://scales.r-lib.org/)
- [viridis](https://cran.r-project.org/web/packages/viridis/vignettes/intro-to-viridis.html)
