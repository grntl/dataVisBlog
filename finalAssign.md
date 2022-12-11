# Final Assignment
[Home](/README.md) | [Visualization Blogs](/vizBlogs.md) | [Short Form Posts](/shortForm.md) 
***
## Our housing and the people who live in them

Every day, we step out from our homes and on our commutes we pass by more homes. Often, we hardly pay attention to those buildings that pass by, but inside each structure holds the livelihoods and abodes of many. Because housing helps satisfy the basic human need for shelter, we must think carefully about what we build. This means understanding how what we build impacts the people that live in them, who tends to choose what kinds of housing, and what kinds of people tend to live in certain housing.

Gaining understanding on the issue of housing can help us literally build a better society for those who might need it the most. Some of those who might need housing the most are those in the market for affordable housing. Affordable housing has become a touchstone issue across America, and various political leaders have been rushing and struggling to resolve a critical lack in affordable housing in the face of rising rents and costs. For example, Mayor Eric Adams in New York City has been putting together a plan to streamline housing development. According to the [New York Times article](https://www.nytimes.com/2022/12/08/nyregion/eric-adams-nyc-affordable-housing-crisis.html) on this issue, “the average rent on newly leased apartments in Manhattan soared past $4,000,” while “[h]omelessness in the city has also reached a record.” In Boston, [city leaders are pushing Mayor Michelle Wu](https://archive.vn/2vcqV) to increase the affordable housing allotment in new developments to a minimum of 20%. These examples demonstrate just how consequential and important housing is, and how it intersects with socioeconomic factors like income of the buyer and price of housing.

To investigate the issue, we use the dataset from the [American Housing Survey: Housing Affordability Data System](https://www.huduser.gov/portal/datasets/hads/hads.html), specifically the ASCII dataset from 2013, which contains data from around 1920 until 2013. This data was collected by the Department of Housing and Urban Development’s Office of Policy Development and Research. [The data contains both housing types and socioeconomic data](https://www.huduser.gov/portal/datasets/hads/HADS_doc.pdf) such that a data analysis like this can understand housing trends for how populations of various socioeconomic statuses are distributed in different forms of housing.

### Is multi-family housing more affordable?

There is a fair amount of publicity of the (N)ot (I)n (M)y (B)ack(Y)ard (NIMBY) attitude that often seeks to oppose denser, multi-family housing in traditionally low-density or single-family housing. A [paper from the Joint Center for Housing Studies at Harvard University](https://brockton.ma.us/wp-content/uploads/2020/08/Overcoming-Opposition-to-Multifamily-Rental-Housing.pdf) states that some of the opposition comes from the idea that building multi-family housing will decrease home values for single-family neighborhoods. Just one example of this is in D.C., [where wealthy D.C. suburbs are fighting against multi-family housing](https://archive.vn/N9qtA/again?url=https://www.washingtonpost.com/dc-md-va/2022/12/10/zoning-single-family-detached-neighborhood/). So just how do prices compare between single-family and multi-family hosuing?

To investigate this, we plotted the average market value by structure type in **Figure 1**. There are many issues with how this variable is coded. Unfortunately, the documentation for the dataset is not entirely comprehensive, and there are many things that are unexplained for which this data analysis has had to work around. In this case, there were many multi-family structures which were given a market value of “-6,” which does not exactly make sense. Further investigation of the data revealed the all the -6’s corresponded with rental units, which means that the actual positive values corresponded to housing for purchase. Either way, the observations of -6 were excluded. Additionally, the numbers appear to be rounded by at least the hundreds, and there appears to be a hard cap at $2,520,000 such that homes over that value might have been given that number.

![Figure 1 Barplot of average market value](https://user-images.githubusercontent.com/114178136/206899156-7683b21b-0ca8-4baa-bf96-3a1105e5f5ce.png)
***Figure 1** Barplot of average market value*

We can see in **Figure 1** that the market value of units are not necessarily highest in single-family homes, despite the contextual evidence stating that the these tend to be wealthy enclaves. Instead, market values tend to be higher for units in larger unit housing structures.

One likely explanation is that multi-family housing tends to be built in cities, as cities are space-constrained, and dense. To test if this explanation is correct, we use a location variable. Once again, the data is very limited, as the location variable only codes for either “Central City” or “-5.” As to what the -5 means, unfortunately, the codebook fails to provide any explanation. The data analysis here takes a leap of faith in assuming that all “-5” codes are for non-Central City locations. By doing so, we produced the graphs in **Figures 2** and **3**. **Figure 2** is a 100% stacked barplot. We can see in **Figure 2** that the majority of multi-family housing units are in cities. Housing in cities tend to be more expensive due to the large amounts of people creating demand. This is proven in **Figure 3**, where market values are much higher for housing in central cities as opposed to elsewhere. This does not hold true for single-family housing, which is very interesting, as single-family housing structures in a city would be quite desirable.

![Figure 2 100% Stacked barplot by structure type](https://user-images.githubusercontent.com/114178136/206899214-eca742c4-13c3-4071-89f8-cdabbc08cf8c.png)
***Figure 2** 100% Stacked barplot by structure type*

![Figure 3 Barplot of average market value by structure type and location](https://user-images.githubusercontent.com/114178136/206899227-d5c48a25-b41f-4662-b66d-834d12054e57.png)
***Figure 3** Barplot of average market value by structure type and location*


Note that **Figure 3** features error bars, which show the 95% confidence interval. These help provide additional information on the difference in number of observations between each category of structure type. Those categories with less observations tend to have greater variance and are slightly more affected by outliers. **Figure 4** presents a simple visualization of the distribution of observations between each category. The categories with smaller amounts of observations do correspond to higher variance as appears in **Figure 3**. This is something to keep in mind for this data analysis.

![Figure 4 Barplot of observations by structure type](https://user-images.githubusercontent.com/114178136/206899235-ddd6cd01-9f53-461c-b969-968f89361ffe.png)
***Figure 4** Barplot of observations by structure type*

The mobile homes proportions in **Figure 2** are a cause for concern. According to the National Alliance to End Homelessness, “[only 25 percent of Americans live in major cities, but 50 percent of people experiencing homelessness are in these areas](https://endhomelessness.org/demographic-data-project-geography/),” but as the graph shows, the large majority of mobile homes are outside of central cities. However, our previous data analysis has shown that mobile homes are consistently the cheapest option across both rental and buyers’ markets where other categories varied. These structures should be a potential solution that policymakers look into.

**Figure 5** use a fair market rent variable provided by the dataset. The dataset actually gives every single observation a fair market rent value, including those homes which were bought that we just looked into. This actually makes it a somewhat more reliable variable to use in looking at housing prices, as it is complete. The remainder of the analysis will rely heavily on this variable.

For the purposes of **Figure 5**, we take the average fair market rent as an aggregated assessment of the value of that type of housing, regardless of whether the home is rented or bought. Accordingly, we can see that single-family housing is more expensive than all the other types of housing. This more closely corroborates the contextual information from the media that state that single-family housing tends to be expensive, which perhaps naturally leads to a wealthier population.

![Figure 5 Barplot of average fair market rent by structure type](https://user-images.githubusercontent.com/114178136/206899241-5de59001-6dfd-4835-8099-68008709191d.png)
***Figure 5** Barplot of average fair market rent by structure type*

![fig6](https://user-images.githubusercontent.com/114178136/206899245-544b2510-3302-4810-96c0-2023e31064a5.png)
***Figure 6** Barplot of average fair market rent by structure type and location*

**Figure 6** shows how the difference in average fair market rents between the city and outside the city. We can see again that housing is more expensive in the city than outside, this time specifically for rental prices.

This information can be important to policymakers on the national or state level. Urban versus non-urban landscapes are quite different in terms of the housing landscape, between both prices and the types of structures. Laws and regulations should keep that and avoid a blanket-fits-all approach. Additionally, if we are to look momentarily look past the flaws in the market value variable, the fact that prices for renters and buyers don’t really seem to match perhaps actually portrays an important fact. [Evidence suggests that rents and prices likely correlate](https://www.forbes.com/sites/richardmcgahey/2022/03/25/inflation-soaring-rents-and-the-housing-crisis/?sh=e0e791a16f57), and perhaps they do when everything is aggregated together, but rents and purchase prices are not necessarily tied together for different structure types. This means that policymakers need to carefully evaluate whether their market is predominantly a rental or buyers’ market before making decisions.

### Who lives in these homes?

If policymakers ought to understand the makeup of their housing market between renters and buyers, the proceeding analysis takes on that task.

**Figure 7** is another 100% stacked barplot, this time showing the proportions of whether households in the different structure types are renting or have bought their home. The results are quite drastic. Single-family and mobile homes are overwhelmingly owned by those who reside in them, and multi-family homes are overwhelmingly rented by their residents.

![Figure 7 100% stacked barplot of owner/renter status by structure type](https://user-images.githubusercontent.com/114178136/206899256-33d1622d-dc37-4ac0-b324-8ab1e0784976.png)
***Figure 7** 100% stacked barplot of owner/renter status by structure type*

We previously looked at average fair market rents as a measure of the overall price of different housing structures, but now we want to understand how the price of housing differs between rental and owned properties To combine this with our previous analysis, **Figure 8** shows the average fair market rents, but distinguishes between whether the property is being rented or bought.

![Figure 8 Barplot of average fair market rent by structure type and owner/renter status](https://user-images.githubusercontent.com/114178136/206899260-98d0aeaa-57a0-49c3-8b2b-f07f34e2d4a9.png)
***Figure 8** Barplot of average fair market rent by structure type and owner/renter status*

Clearly, bought properties are more expensive for every structure in comparison to rental properties. Accordingly, multi-family housing built for rental purposes can potentially help decrease home prices.

How do these prices reflect on homeowners? **Figure 9** has boxplots for each structure type showing cost burdens. Cost burden is a variable that is calculated by taking the monthly cost of housing and dividing it by monthly income. **Figure 9** does not distinguish between rental and owned properties. There are again limitations to the data. The first is that many observations of the variable are coded as “-9” and “-1.” This does not make any sense in the context of the calculation. It is partially explained in this note by one of creators of the dataset, which states that the -1 values represent incomes which were reported as zero or negative. Regardless, all negative values were excluded from the analysis in **Figure 9**. The second is that the large majority of the data falls between 0 and 1, but there are some outliers that are enormous. Including them into a boxplot would make the boxplots unreadable. This is demonstrated in **Figure 10**. But as can be seen in **Figure 10**, the outliers themselves show an interesting decreasing trend from single-family housing over into multi-family housing. This is again, likely highly influenced by the difference in the number of observations in each category, as more observations in a certain category often lead to a higher raw tally of outliers. While this analysis does not take upon any analysis or interpretation of these outliers, **Figure 10** was included just as something at least worth noting.

![Figure 9 Boxplots of cost burdens by structure type](https://user-images.githubusercontent.com/114178136/206899271-09ef30c0-2432-41d3-bff4-dade790c59dc.png)
***Figure 9** Boxplots of cost burdens by structure type*

![fig10](https://user-images.githubusercontent.com/114178136/206899276-2a6cbdd6-a820-4bb2-8923-907a3d9b5297.png)
***Figure 10** Boxplots of cost burdens by structure type (w/o filtering out burdens > 1)*

![fig11](https://user-images.githubusercontent.com/114178136/206899280-8168d1cf-4231-4506-902f-ab8deb977c6f.png)
***Figure 11** Boxplots of cost burden by structure type and owner/renter status*

**Figure 9** shows that cost burdens are higher for multi-family housing than single-family housing or mobile homes. This is despite the fact that we saw in **Figure 5** that housing is cheaper for multi-family housing. **Figure 11** depicts the data from **Figure 9**, but distinguishes between owner and renter. The distinction is important, as those who rent properties have consistently greater cost burdens, despite rent being cheaper, as shown in **Figure 8**. If housing is cheaper for multi-family housing and rental properties, yet the cost-burden is higher for multi-family housing and renters, then perhaps the missing link is that those who are in the market for multi-family housing and/or are renters have lower incomes.

![Figure 12 Barplot of average adjusted income for number of persons by structure type and owner/renter status](https://user-images.githubusercontent.com/114178136/206899291-dd5e2ce9-c7e2-44bc-80c2-afed650ecb14.png)
***Figure 12** Barplot of average adjusted income for number of persons by structure type and owner/renter status*

**Figure 12** shows the average adjusted income for the number of persons in the household by structure and whether the property is between owned or rented. As we can see, the adjusted incomes are always higher for those who own housing. This seems to match **Figure 8**, as households of lower incomes are in the rental market where prices are cheaper, compared to wealthier households in the buyers’ market where prices are higher. Moreover, **Figure 8** shows that the larger the structure type, the lower the household income. This confirms the contextual evidence and also casts a different light onto **Figure 9**. If cost burden is calculated using income, it seems like a given that income is the missing link between cost burden and housing prices. But as this analysis as shown, income and prices do not trend as one-to-one as their individual graphs might suggest, or else the cost burden boxplots in **Figure 9** would have been more steadily even across the board. However, multifamily structures are clearly slightly higher than single-family housing and mobile homes. This means that those who are in multi-family housing are having a comparatively more burdensome time affording their housing.

### The ones who need it the most

In the data cleaning done for **Figure 9**, values below 0 for the cost burden variable were excluded. However, they marked out important information: negative values were given to incomes that were reported as zero or negative. By investigating specifically that subset of data, we might be able to learn more about who lives in what kinds of housing. **Figure 13** conveys much the same information as **Figure 12** but displays the lowest values, which for the adjusted income variable are also negative (but appear as 0 on this graph). To note, unlike the cost burden variable, these values for the adjusted income variable were not excluded from previous graphs. A negative value for cost burden would represent someone who probably struggles most severely with cost burden, but it would have decreased the cost burden values if included. However, a negative value for adjusted income would pull down any measures like mean or median as they probably would in their original number before given the coding of “-9.” In a way they make the data “more accurate.”

![Figure 13 Boxplots of adjusted income for number of persons by structure type and owner/renter status](https://user-images.githubusercontent.com/114178136/206899301-0cc38200-34ec-493b-a645-92adb50b7493.png)
***Figure 13** Boxplots of adjusted income for number of persons by structure type and owner/renter status*

To investigate the negative values, we filtered everything else out, and graphed them by counts. To achieve this, we had to do more data cleaning. The documentation states:

"an unusually high proportion of households reports zero or negative incomes, compared to other surveys. To partially correct for this bias, households that report zero or negative incomes but are living in adequate, uncrowded units and paying at least the Fair Market Rent in housing costs are assigned to the income category 5 (≤ LMED)"

Accordingly, the values which were assigned category 5 were filtered out. **Figures 14** and **15** show that those with zero or negative income are overwhelmingly renters. **Figure 14** uses data from the adjusted income variable, and **Figure 15** uses data from the cost burden variable. Renters are the ones struggling most acutely, and also in less acute ways, across the board. Policymakers should focus on helping this specific demographic.

![Figure 14 Barplot of no or negative income by structure type and owner/renter status](https://user-images.githubusercontent.com/114178136/206899303-e3842438-0815-4bfa-bdf7-60ca87a16013.png)
***Figure 14** Barplot of no or negative income by structure type and owner/renter status*

![Figure 15 Barplot of no or negative income (BURDEN) by structure type and owner/renter status](https://user-images.githubusercontent.com/114178136/206899307-b1488034-90bc-42c0-93ee-06add546b1d1.png)
***Figure 15** Barplot of no or negative income (BURDEN) by structure type and owner/renter status*

### The future

This analysis has yielded several things that policymakers and anyone interested in this issue should keep in mind.

1. Renters struggle comparatively more than buyers across the board.

2. Multi-family housing tends to be the cheapest

3. Multi-family housing is overwhelmingly a renters’ market.

4. Based on 1-3, multi-family housing should likely yield the most attention in terms of our housing policies.

5. Mobile homes could be really helpful

Housing is not only essential, many people and organizations, [such as the UN](https://www.ohchr.org/en/special-procedures/sr-housing/human-right-adequate-housing), argue that housing is a human right. Affordable, quality housing should be a priority for everyone.

### Citations
Link to citations: https://github.com/grntl/dataVisBlog/blob/main/finalProjBib.pdf

