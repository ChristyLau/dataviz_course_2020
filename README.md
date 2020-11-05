[click here to see the prototype]( https://yaozheng600.github.io/DataViz_course_2020/)

Worked with Zheng Yao, Jaleed Aslam and Jiale Cheng

# PROJECT DOCUMENTATION
## 1. CONCEPTS of OUR WORK     
Our work is mainly to study the changes in the stock market during the epidemic, focus on the situation of global stock market and explore the reasons of significant differences of stock development among countries and companies through data visualization. And give investment advices.
## 2. DATA SOURCES
We use COVID-19 data provided by [Data on COVID-19 (coronavirus) by Our World in Data](https://ourworldindata.org/coronavirus). And data of stock provided by:[Yahoo Finance](https://finance.yahoo.com) and [Investing.com](https://www.investing.com). We crawling the following data from this two webseit:
* 62 general equity market indices from 43 countries
* 500 Companies’ history and info from US (S&P 500)
* 438 group of  companies' history and info from Europe (MSCI Europe)
* 300 Companies history and info from China (CSI 300)
* Top 500 companies of the world by ranking         
        
license information:
* [Yahoo Finance](https://github.com/scheb/yahoo-finance-api/blob/4.x/LICENSE)
* [Investing.com](https://www.investing.com/about-us/terms-and-conditions#special_conditions_money)

## 3. DESIGN DECISIONS
### 3.1 Domain problem characterization        
The target users are stock market investors and people who interested in the economy during the COVID-19 period. The domains of interest are the stock market and the epidemic. The questions are how to invest during the epidemic, and to explore the state of the world economy through the stock market. The data related to the problem is divided into two aspects. One is the data regarding to the epidemic situation in each country, including new cases, national policies, medical conditions, and aging degree etc. The second is the price changes at different levels of the stock market, including national stocks, stock sectors, and company stocks. 
### 3.2 Abstraction    
Based on the problem domain, we are concerning about the price changes of all levels of the stock market (countries, sectors, companies) over time in the context of the epidemic. And find the correlation between the epidemic and the stock market. From this we can roughly determine the object of data abstraction: 1. The changes in the stock market at three levels. 2. The severity of the epidemic and the factors affecting the development of the epidemic in various countries. 3. Describing information about different aspects of a company.   
#### 3.2.1 Data abstraction
We use the change rate of the stock market's price relative to the price at start time to express the change in the stock market. The start time is February 19, 2020, which is the start of the global pandemic of COVID-19. We calculate it as the fomular:     
![](https://latex.codecogs.com/gif.latex?growth_t=\\frac{Price_t}{Price_{19.Feb.2020}}-1)      
We use the positive rate to express the severity of the epidemic, and the way to aggregate data is to take the average of the products. In addition, the factors affecting the development of the epidemic are GDP, the stringency of policies, the average age of the population, and the number of hospital beds per thousand people， which can be quantified numerically.      
We use information such as the number of employees, the enterprise value, and the profit margin to describe a company. This information can also be obtained directly.      
#### 3.2.2 Task abstraction
The abstraction of tasks is still divided into three levels to discuss. At the national level, firstly, our task is to find how each country's stock market changes over time. And it can be compared between different countries. Here we design two filters to filter different continents and different countries to focus on countries of interest. Secondly, in order to find the correlation between the stock market and the epidemic, we selected several representative countries as a comparison, and explore the correlation between the stock market change rate and various epidemic-related factors.      
At the sector level, our task is to find the composition of 11 stock sectors in a specific country and their changes during the epidemic.       
At the company level, our task is to find out what kind of companies performed well during the epidemic. We need to find the correlation between the rate of change of the stock market and the description information of each company, and perform cluster analysis according to the country to find the overall performance of the company within this country.
### 3.3 Visual encoding / interaction design     
According to task abstraction, we extracted the following tasks:
1. The changes in the stock market of each country over time, and the horizontal comparison between countries.
2. the correlation between the stock market and the epidemic
3. composition of 11 stock sectors in one country and their changes.
4. the correlation between the stock market and companies.        

The first task is not only the stock market changes over time, but also the comparison between different countries on each continent. A single chart cannot accomplish all these tasks, so we use multi-view to achieve it. First, we use a bar-chart as subchart 1 to show the stock market changes in each continent: the x-axis represents the stock market change rate, the y-axis represents each continent, and the chart is sorted in descending order of the stock market change rate for comparison. And we add "hover mouse" interaction to enable readers to focus on the specific data of each continent. Sub-chart 2 is a line chart of changes in the stock markets of various countries over time. The x-axis represents time and the y-axis represents the rate of change of the stock market. The line chart can well reflect the change process of different countries during the whole period. There are too many countries' data in sub-chart 2, in order to focus on a single country, we apply a filter to select a specific country. First, click on the continent where the country of interest is located in sub-chart 1, and the corresponding sub-chart 2 will show all countries in that continent Changes in the stock market. At the same time, sub-chart 3 will show a bar chart of the rate of change in the stock markets of all countries in the continent. We click on the country bar of interest to focus on the changes in the stock market of a specific country over time, and use a line chart(sub-chart 4) to show it. In sub-chart 4, we have added a reference line so that readers can easily focus on the rate of change of the stock market at each time point. In general, sub-chart 1 and 2 are used to show the overview, and the semantic zooming is achieved by clicking on the bars. In sub-chart 3 and 4 we can get the detailview.               
In Task 2, we use a scatter plot to show the correlation between the stock market and the epidemic in order to find clusters and outliers. The x-axis represents a quantified factor affecting the epidemic, the y-axis represents the rate of change of the stock market, and each scattered point represents a country. We selected 6 influencing factors: stringency index, hospital beds per thousand, human development index, gdp per capita, median age and positive rate. We use these 6 scatter plots as sub-charts to form a small multiples together. We added geografical zooming to each sub-chart to clearly show clusters and outliers, or focus on the details of the data in a specific country.       
Regarding the task 3, we first thought of using a pie chart to show the share of each sector. However, there are 11 sections in total, and there is not much difference between the percentages of some sections, the data cannot be displayed well. We still choose grouped bar chart in the end. The x-axis represents 11 sectors, and the y-axis represents the stock market price. Each set of bars displays the start time and end time of the price in this sector. We can not only compare the shares by the length of the bars, but also show the changes of each sector through the changes in prices within the group. At this time, we are still not sure about which country's sector data will be displayed. It depends on the results of our analysis of the data after completing tasks 1 and 2.       
Task 4 and Task 2 are similar in structure. So we use the same visual encoding. The small multiples represent different company descriptions in the vertical direction, and different countries in the horizontal direction to create a control group. Regarding the interaction, you can still use zoom in to discover clusters, or focus on an outlier to get detailed information by hover your mouse.      
## 4. POSSIBLE IMPROVEMENTS        
You may have noticed that we have a problem in the design of the interaction: if you don't read the text, it is difficult for readers to think of clicking each bar in the bar chart to use the filter. To solve this problem, we consider that we can set check boxes to filter different countries. In this way, the readers can see  the interactions they can use.
## 5. USER GUIDE of THE PROTOTYPE
[![Watch the video](https://img.youtube.com/vi/7z7VXcybZ7c/hqdefault.jpg)](https://youtu.be/7z7VXcybZ7c)
