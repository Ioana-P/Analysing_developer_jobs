# Exploring the Software Developer job market through Indeed job posts

I scraped 498 job posts from Indeed.co.uk, searching for "software, developer" in the title, and then analysed the data. 
### **TL;DR**
###### If you take my word for it, here's what I found: 
1. JavaScript (and its variants), Python and Java were the most popular languages mentioned.
2. Most jobs are concentrated in London, predictably, with the next most popular location being the emerging mini tech-hub of Cambridge. 
3. There is no significant reason to believe that job posts mentioning a particular programming language will be higher or lower paid (at least as far as this sample can tell).
4. 



### Problem(s): 

### Plan:

### Data:
*
### Analysis:
* 
### Conclusion: 

###### 1. 
###### 2. 
###### 3. 


This project was undertaken for 3 reasons: 
1. To investigate and test hypotheses about Data Scientists, Data Analysts and ML Engineers;
2. To test presuppositions about the job market for Data Scientists / Analysts ML Engineers and
3. To demonstrate and practice data retrieval via webscraping. 

*One important caveat I must mention about the data is this: although all of the data neatly categorised as either DS, DA or MLEng is shown clearly in my data analysis and exploration, if you had to go through each job post by title you will find plenty that say "Business Analyst", "Data Engineer" or "Data Science Researcher". This is because the main method by which the data was extracted was by entering the search terms and thus the jobs are categoried **by which search term retrieved them**. This speaks volumes to the fact that:
a) there is significant semantic overlap between these terms;
b) Many such job posts include the job search terms not in the title but in the description and 
c) That our data acquisition process relies on the inner functioning of indeed.co.uk's internal search engine.

###### Therefore I retrieved Data Scientist and ML Engineer job post data from Indeed.co.uk in late May 2020 using Selenium webdriver and BeautifulSoup. The same was done on 23rd of June for Data Analyst
###### I wrangled and analysed the data in Pandas, MNLTK, Seaborn and Matplotlib. 


##### Here are 3 concrete questions I wanted to answer with this project:
1. How many job posts for this sector advertise their salary?
2. Are there any skills that differentiate the two types of job?
3. How many of the jobs seem to indicate that remote/flexible working is an option?

# Findings in brief (this list is still being expanded):





To check the topics yourself, run the `LDA_viz_plot.html` file in this repository. I recommend setting the lambda parameter (accessible via the slider in the top-right) to a value between 0.4 and 0.6. 

For a more in-depth explanation of how Latent Dirichlet Allocation works and how to interpret pyLDAviz fully, see [my previous article](https://towardsdatascience.com/latent-dirichlet-allocation-intuition-math-implementation-and-visualisation-63ccb616e094).



References:

* ONS Sector Data - https://www.ons.gov.uk/filters/c60ed96a-df5b-4dbe-bbda-ab407c9639d6/dimensions 
* SlashData Report - 'State of the Developer Nation 19th Edition' - https://slashdata-website-cms.s3.amazonaws.com/sample_reports/y7fzAZ8e5XuKCL1Q.pdf 
*  Assumptions of Point Biserial Correlation - https://statistics.laerd.com/spss-tutorials/point-biserial-correlation-using-spss-statistics.php
* Point Biserial Correlation with Python - https://towardsdatascience.com/point-biserial-correlation-with-python-f7cd591bd3b1


Key Assumptions to bear in mind:
* **Data sourcing** - Data was sourced purely from Indeed.co.uk over a limited time span. The individual time of scraping is recorded for each job post inside the raw_data file raw_data/SE_jobs_20_11_2020.csv. Further sampling over time will be needed to replicate or falsify findings.
* **National averages** - ONS data was filtered to retrieve data for 2019 as 2020 data is a. not fully available yet broken down by and b. 2020 survey data was affected by the Covid19 lockdown and the move to telephone polling. Although the 2019 mean salary is not a fair comparison for data retrieved in Q3 2020, it provides a rough benchmark against which we can compare our sample. 
* **Data mining** - The salary extraction method is reliant on the pattern finding of text that "looks like salary data" - i.e. the python script that I wrote searched specifically for text that included "£" followed by any length of numbers (continuous or punctuated by a comma) and a time period phrase such as "per day", "per annum", "a year", etc. Spot-checking showed the method to be robust. Where a range was stated (e.g. "£40,000 - £50,000") the mean was taken. 
* **Webscraping process** - The webscraping tool generally managed to retrieve the maximum of 19 jobs posted per page on Indeed's search result pages. The first part of the scraping had a human-in-the-loop (i.e. myself) monitoring the scraper navigating the page, to ensure data retrieval quality. Occasionally, due to an unforeseen pop-up or a nested html element, I had to scroll the automated Chrome browser in the right direction so that it would carry on retrieving new job post URLs. However, this means that some job posts may have been overlooked. This shouldn't pose a significant problem, since I was sampling from the much larger number of total available job posts, but the sampling method's randomness is reliant on the order in which Indeed presents results. 
* **Searching by title** - 