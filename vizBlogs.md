# Visualization Blogs
[Home](https://github.com/grntl/dataVisBlog/blob/eb6b53ed750a854b63c563fde42f9b9ebcaddfd0/README.md) | [Short Form Posts](https://github.com/grntl/dataVisBlog/blob/b1541ee35cb8d109bd1438eee7f3d958f1790daa/shortForm.md) | [Final Assignment](https://github.com/grntl/dataVisBlog/blob/9fd117a4d77a7aaa432f277695ff197ed8c54b8a/finalAssign.md)
***
## A visualization I found recently that I disliked
I found this data visualization on from a [Wall Street Journal article about carbon emissions](http://graphics.wsj.com/climate-talks/). 
![Web capture_10-10-2022_04257_graphics wsj com](https://user-images.githubusercontent.com/114178136/194805121-7aff6336-04ab-4de9-8db5-ec44181f2801.jpeg)

I dislike this visualization because for a rather simple reason. I understand that the countries are in order of largest to smallest carbon emitters, but the groupings make it seem as if the EU and India had something in common other than that, and especially for the last group. There's no way they couldn't have done this without grouping them in that way. Also, I'm fairly confused at how they are ordered the way they are when Indonesia's units are lower than some below it in the rankings. It is cool to put the visualization in the shape of the countries, but I would have preferred the squares just be stacked up in nice bars in order of largest emitters to smallest. It's simpler and easier to understand. 
## A visualization I found that I liked
![Web capture_10-10-2022_222639_archive ph](https://user-images.githubusercontent.com/114178136/194990371-747ee777-205c-4425-a8f1-ac75da6bba2a.jpeg)

I found this from a [New York Times article about abortion costs](https://archive.ph/NKrTS). I liked this visualization because it kept the y axis consistent throughout every single graph despite the fact that there were many of them and that one even went off the chart. In my opinion, that's preferable to having a different y-axis for every single graph because then it would be hard to evaluate or compare across graphs. 

A bit of code that might produce the same thing with two graphs would be:
```
abortionClinic1 %>%
  ggplot(aes(x = year, y = avg_spendingPerPatient)) + 
  geom_line() +
  ylim(0, 1000)
```
