**2024/10/30**<br>
**Mpad 2003 Data Storytelling**<br>
**Maxine Zeng**<br>
**Presented to Jean-Sébastien Marier**<br>

# Midterm Project: Exploratory Data Analysis (EDA)

## Foreword

This data exploratory analysis focus on learning objectives of data storytelling:

`1.` Import, cleaning data from scratch
`2.` Learning basics of github 
`3.` Learning how to write markdown files

<!-- * [GitHub's *Basic writing and formatting syntax* page](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

Did you notice how to create a hyperlink? In Markdown, we put the clickable text between square brackets and the actual URL between parentheses.

And to create an unordered list, we simply put a star (`*`) before each item. -->

## 1. Introduction

This exploratory data analysis will be analyzing the City of Ottawa dataset of citizen requests.
The City of Ottawa receives requests from four sources: 311 contact centre, client service centre, 311 email and web-based self- service portal. Which includes variety of content such as from Bylaw Services, Citizen Services, City Facilities and Garbage and Recycling, etc. It includes attributes of Service Request ID, Status, Description, Type, Opened Date, Closed Date, Address, Latitude, Longitude and Channel. They collected these requests and documented each one of them down into a dataset. The dataset is meant to update daily.

This analysis will including sections of getting data, understanding data, potential story, conclusion and references list.

* [Link to the original dataset from City of Ottawa (updating daily):](https://open.ottawa.ca/documents/65fe42e2502d442b8a774fd3d954cac5/about)

* [Link to the csv version I used.](https://raw.githubusercontent.com/jsmarier/course-datasets/refs/heads/main/ottawa-311-service-requests-august-2024.csv)

<br>

## 2. Getting Data

First, I download the data from the github link assigned with a shortcut Ctrl + S, place it under my github folder. Then open google sheet, select tab "file", then "import", upload the file from saved location.


![](./images/Screenshot-after-import-dataset.png)<br>
*Figure 1: The imported dataset in Google Sheets.*
<br>

* [Link to my dataset imported in Google Sheets](https://docs.google.com/spreadsheets/d/1mhltDAwbRGIJIhvvtqf18TT1oe3h3seDmpCdTad6e7E/edit?usp=sharing)

From A to K, there are 11 columns and 28539 row of data for each individual cases. Apparently, the original dataset is quite overwhelming for analyzing. The data looks quite clean and well structured, but it can still benefit from some modification for a clear readability. 

The variables in different columns can be identify as following:

`1.` Categorical variables: refers to a value that can not be quantifiable, either nominal or ordinal. 
`2.` Nominal variables: One that describes a name, label or category without natural order. 
`3.` Ordinal variables: The value can be defined with an order relation in between.
(Statistic Canada, 2020)

Identification for specific columns: 

`1. ` Column A "Service Request ID | Numéro de demande" contains numerical ordinal ID numbers, which are all unique to its own case.

`2. ` Column B "Status | État" contains nominal categorical data, which only has "Resolved", "Cancelled" and "Active" as input, they have no order relation in between.

`3. ` Column C "Type | Type" is nominal categorical data defining the request under a big category. It has 11 categories in total.

`4. ` Column D "Description | Description" Contains 554 sub category data under each big category, which is also nominal categorical data.

`5. ` Column E "Opened Date | Date d'ouverture" and Column F "Closed Date | Date de fermeture" are ordinal date data, there will always be a specific opened data on column e, but Column F can be mark as "/N" because it is not resolved.

`6.` Column G "Address | Adresse" includes text information of address that are nominal. A lot of them were marked as "\N".

`7.` Column H "Latitude | Latitude" and I "Longitude | Longitude" are discrete data indicating the coordinate of the address. Can be marked as "\N" with address

`8. ` Column J "Ward | Quartier" is 24 ordinal categorical data of the ID of wards in Ottawa, but some of them were marked as "\N" as the 25th category. The ID of wards makes the data cleaner and easier to use compare to data record with ward names, which may have different versions.

`9. ` Column K "Channel | Voie de service" is nominal categorical data of how the case being requested, there are 6 category in total.


After understanding the data, I wonder if there is a correlation between wards and type categories of issues.

* [Statistics: Power from Data! 4.2 Types of variables](https://www150.statcan.gc.ca/n1/edu/power-pouvoir/ch8/5214817-eng.htm)

<!-- Use two hashtag symbols (`##`) to create a level 2 heading like this one.

To include a screen capture, use the sample code below. Your images should be saved in the same folder as your `.md` file.

![](./images/import-screen-capture.png)<br>
*Figure 1: The "Import file" prompt on Google Sheets.*

=IMPORTHTML("https://en.wikipedia.org/wiki/China"; "table", 5)
```
This also shows how to create an ordered list. Simply put `1.` before each item. -->

<br>

## 3. Understanding Data

### 3.1. VIMO Analysis

This VIMO Analysis is focusing on Column C Type, Column D Description and Column J Ward Columns:

`1. `Valid: 

Valid data meets 3 conditions: It is not blank or missing, it is within a valid range, and it is correct.(Statistics Canada, 2020)

Most data are valid under each category except for the missing ones. 
They are identify as Micro data, which are summarized into a big category.

`2. `Invalid: 

Invalid data refers to certain unreasonable or impossible value under a specific category.(Statistics Canada, 2020)
I check through Google sheet's inside column stat and filtering, there are no data seems to be Invalid except for the missing ones.
    
`3. `Missing: 

Missing data means the cell was left with blank.(Statistics Canada, 2020)
In our dataset missing values are marked as "\N".

There are 1549 rows of data is being marked as "\N" under column of wards. 
There are 628 rows are being marked as "\N" under column Description
There are 2 rows of data being marked as "\N" under column of types.

* [Data Accuracy and Validation: Methods to ensure the quality of data](https://www.statcan.gc.ca/en/wtc/data-literacy/catalogue/892000062020008)

`4.`Outlier: 

Outlier in a dataset refers to a value that is either extremely large or small. (Statistics Canada, 2020)

I noticed that for the type Water and the Environment, there are 834 row of ward ID being marked as missing, which is noticeably higher than other types. This problem could be due to location ambiguity, which some issues location were not clearly defined within ward boundaries or have cross ward boundaries, leading to reporting confusions. 


<!-- Support your claims by citing relevant sources. Please follow [APA guidelines for in-text citations](https://apastyle.apa.org/style-grammar-guidelines/citations).

**For example:**

As Cairo (2016) argues, a data visualization should be truthful... --> 
<br>

### 3.2. Cleaning Data

To clean the data, I duplicated the original dataset into a new sheet called "Type and ward", then I hided most of the columns except the three columns (Type, Description and Ward) that I needed. Then I removed all the French labels after the divider for each column on first row. Next, I selected the first row and freeze them as my header, they will stay on top of when I scroll down. 

For the Type column, I found all the "and" using the find functions with Ctrl F, the replace all of them to a divider " | ", resulting a shorter value for each row with more clear readability. After that I removed all of "the" for the same purpose. Then I sorted the data from A to Z in Type column.

For the description tab, I placed spilt functions `=SPLIT(D2, "|")` to split the French description to two extra columns. Then I copy the value in the English description column with Ctrl + Shift + V to copy plain text only to get rid of the split formula. Then deleted the French description column and the original one. This action refers to the data cleaning tutorial in week 5, which have made the table looks cleaner and simpler. (Marier, 2024)                 

I further split the description tab with `=SPLIT(D2, "-")`, which splits it into 3 columns. Then I copy and pasted the three column as plain values, then I rejoin the last two columns together with `=CONCATENATE(F2," ", G2)`. The concatenate column is named as Sub description, which is useful for looking at data within a smaller range then the original Description categories. Then I used the trim white space tool under the data cleaning of Google onto the new Description and Sub Description column.

* [MPAD 2003: 5.1 Cleaning Data in Google Sheets](https://brightspace.carleton.ca/d2l/le/content/290806/viewContent/3855132/View)

<br>

### 3.3. Exploratory Data Analysis (EDA)

The cleaned dataset now only includes four column, Type, Description, Sub Description and Ward. Which I can used to see patterns of the issues between wards.

A pivot table `Type and Ward Stats` was created to analysis the relationship between Wards and Type. Which only contains nominal variables. The table is also an ordinal level of measurement with these following requirements met(TouhidulIslam, 2021):
    `1. ` The data classifications of the columns are mutually exclusive and exhaustive.
    `2. ` The data can be meaningfully ranked by its number, from low to high. 

* [Levels of Measurement (Nominal, Ordinal, Interval, Ratio) in Statistics] (https://www.datasciencecentral.com/levels-of-measurement-nominal-ordinal-interval-ratio-in/)

In the pivot table, I also calculated the mean of all Types using `=DIVIDE(AA2, 24)`, and the median with `=MEDIAN((B2:Z2))`. The average of Requests between 24 wards is approximately 1190 per ward. The highest one is ward 12 Rideau-Vanier with 1628 request and Ward 20 Osgoode with 648 requests, the median is 1168 requests from ward 18 Cumberland. 

![](./images/Type-and-Ward-Stats.png)<br>
*Figure 2: This pivot table shows the relationship between Ward and Type*
<br>

Based on the pivot table,  I created a few simple visualizations in Google sheets. In the graph visualizing type of requests per Ward on figure 3, the Garbage and Cleaning category in orange is the most common value. It can also be marked as significant data since it went over 30% of the data.

* [Interpretation of VIMO table](https://umanitoba.ca/manitoba-centre-for-health-policy/sites/manitoba-centre-for-health-policy/files/2021-11/vimo-table-interpretation.pdf)

In the second visualization in figure 4, you can also spot the outlier that was found earlier, which is from Water and Environment that are on the column for requests's ward being marked as missing. 

![](./images/Type-of-Requests-per-Ward-of-Ottawa-in-Percentage.png)<br>
*Figure 3: Percentage of Types*
<br>

I further dived into the missing value in percentage, Citizen Service has 25.3% ward information missing and Water and Environment has 20.1% percentage missing. These two are the only ones that is significantly higher than others.

![](./images/Percentage-of-Missing-Value-in-Wards-for-Types.png)<br>
*Figure 4: Percentage of Types*
<br>

The Licenses | Permit rows are most rare requests among all the categorical, which is not surprising, but Health | Safety row being the second least seems to be odd. 

Covariations happened between the number of the types and the total number of requests per ward. For example, ward 12 Rideau-Vanier has the highest total number (1628) and the most Bylaw Services (611) request at the same time. Ward 20 Osgoode has the fewest number of total number and fewest number of Water Requests. (Wickham 2017)  

* [R for Data Science](https://r4ds.had.co.nz/exploratory-data-analysis.html)

![](./images/Type-of-requests-per-Ward-of-Ottawa.png)<br>
*Figure 5: This graph visualized the type of requests per district*
<br>

![](./images/Ottawa's-Ward-Requests-per-Types.png)<br>
*Figure 6: This graph visualized each district's request number in different types*

<br>

## 4. Potential Story

A potential story in my analysis can be sharing which ward in Ottawa is the most habitable and safe, by analyzing which ward has less issues. For example we can create a heat map using the ward map of Ottawa, using the color red to indicate which wards are tend to be problematic. 

This story can be further narrowed down targeting a certain group, for example the analysis can focus on elders. Then we can focus on types like Roads and Transportation, Health and safety, and Bylaw services that closer binds with their daily life. If a district has high amount of noise complaints under bylaw services, poor road management, and active health concerns, it will be identify as less suitable for elders to live in there.

An example of this type of data storytelling, CTV Ottawa reported noise issue in 2015 ward by ward. The former bylaw Chief Roger Chapman claimed that the most popular noise complaints they received are loud musics, construction noises and machine noises, anything above 50 db is consider violation. The top 1 complaint ward is 12 Rideau Vanier. (CTV Ottawa 2015)

* [What's all the noise? A ward-by-ward breakdown of noise complaints in Ottawa](https://ottawa.ctvnews.ca/what-s-all-the-noise-a-ward-by-ward-breakdown-of-noise-complaints-in-ottawa-1.2431535)

For further information onto my topic, it would be a great help to interview the current city Councillors of Ottawa or bylaw chief, and the local residents who are currently experiencing the issues. 

<br>

## 5. Conclusion

The most challenging part of this assignment is managing to clean the data itself. For a large dataset containing all most 30k rows of data, it is a heavy loaded work for my laptop to process, it glitched and crushed the browser for a few times. Reflecting on this experiencing, I recognized that I needed to narrow down my study to a smaller range with a more focused topic. Thus it would provided me with a lighter data handling.   

On the other hand, the rewarding aspect came after the data cleaning when I created the visualizations. Seeing the data table and visualization turn out to be clear and readable for data storytelling, which all the efforts on the data before them seen well worth it.  

Besides from the the data processing part, I also identified my knowledge gap on analysing the data, I needed to revisit course readings and research for additional resources online to learn and reference how to write more effective exploratory data analysis. Acquiring the new skills for telling a compelling story through data and data visualization made the project feel worthwhile.

In summary, this assignment has been a practice with challenges an rewards, emphasizing the importance of data cleaning and efficiency of data storytelling. 

<br>

## 6. References

`1.` City of Ottawa. (2024, October 3). *2024 service requests. Open Ottawa*. [https://open.ottawa.ca/documents/65fe42e2502d442b8a774fd3d954cac5/about](https://open.ottawa.ca/documents/65fe42e2502d442b8a774fd3d954cac5/about)

`2.` CTV Ottawa. (2015, June 19). *What’s All the noise? A ward-by-ward breakdown of noise complaints in Ottawa.* [https://ottawa.ctvnews.ca/what-s-all-the-noise-a-ward-by-ward-breakdown-of-noise-complaints-in-ottawa-1.2431535](https://ottawa.ctvnews.ca/what-s-all-the-noise-a-ward-by-ward-breakdown-of-noise-complaints-in-ottawa-1.2431535)

`3.` Hong, S. P. (2015, March 27). *Interpretation of vimo table. University of Manitoba*. [https://umanitoba.ca/manitoba-centre-for-health-policy/sites/manitoba-centre-for-health-policy/files/2021-11/vimo-table-interpretation.pdf ](https://umanitoba.ca/manitoba-centre-for-health-policy/sites/manitoba-centre-for-health-policy/files/2021-11/vimo-table-interpretation.pdf)

`4.` Marier, J.-S. (2024, September). *VIDEO | Cleaning Data in Google Sheets*.  [https://brightspace.carleton.ca/d2l/le/content/290806/viewContent/3855132/View](https://brightspace.carleton.ca/d2l/le/content/290806/viewContent/3855132/View)

`5.`Statistics Canada. (2021, September 2). 4 data exploration 4.2 types of variables. 4.2 Types of variables. [https://www150.statcan.gc.ca/n1/edu/power-pouvoir/ch8/5214817-eng.htm](https://www150.statcan.gc.ca/n1/edu/power-pouvoir/ch8/5214817-eng.htm)

`6.` Statistics Canada. (2022, May 11). *Data accuracy and validation: Methods to ensure the quality of data*. Government of Canada, Statistics Canada. [https://www.statcan.gc.ca/en/wtc/data-literacy/catalogue/892000062020008](https://www.statcan.gc.ca/en/wtc/data-literacy/catalogue/892000062020008)


`7.` TouhidulIslam, M. (2021, February 25). *Levels of measurement (nominal, ordinal, interval, ratio) in statistics. Data Science Central*. [Levels of Measurement (Nominal, Ordinal, Interval, Ratio) in Statistics](https://www.datasciencecentral.com/levels-of-measurement-nominal-ordinal-interval-ratio-in/)

`8.` Wickham , H., & Grolemund, G. (2017). *R for data science. 7 Exploratory Data Analysis*. [https://r4ds.had.co.nz/exploratory-data-analysis.html](https://r4ds.had.co.nz/exploratory-data-analysis.html)


<!-- Include a list of your references here. Please follow [APA guidelines for references](https://apastyle.apa.org/style-grammar-guidelines/references). Hanging paragraphs aren't required though.

**Here's an example:**

Bounegru, L., & Gray, J. (Eds.). (2021). *The Data Journalism Handbook 2: Towards A Critical Data Practice*. Amsterdam University Press. [https://ocul-crl.primo.exlibrisgroup.com/permalink/01OCUL_CRL/hgdufh/alma991022890087305153](https://ocul-crl.primo.exlibrisgroup.com/permalink/01OCUL_CRL/hgdufh/alma991022890087305153) -->
