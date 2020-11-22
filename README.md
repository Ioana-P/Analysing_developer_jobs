# Exploring the Software Developer job market through Indeed job posts

I scraped 498 job posts from Indeed.co.uk, searching for "software, developer" in the title, and then analysed the data. 
### **TL;DR**
###### If you take my word for it, here's what I found: 
1. JavaScript (and its variants), Python and Java were the most popular languages mentioned.
2. Most jobs are concentrated in London, predictably, with the next most popular location being the emerging mini tech-hub of Cambridge. 
3. There is no significant reason to believe that job posts mentioning a particular programming language will be higher or lower paid (at least as far as this sample can tell).
4. There are some small, emerging sub-groups of SE jobs that stick out from the group due to nature of the hiring company's work: e.g. software development for bioinformatics and other academic research (centred more in Oxford & Cambridge); SE roles that facilitate finance work and trading, which centre around London.


## In greater detail: 

### **Problem** 
We have our questions about the software developer UK market:
1. How many SE jobs advertise salary?
2. What is the spread of salaries advertised for SE jobs on indeed.co.uk?
3. What are the main locations that SE appear in, other than London?
4. What are some of the most frequent words mentioned in the job title?
5. Which programming languages are in greatest demand?
6. What are the main topics emerging from the job descriptions and the title?
### **Plan** 
Scrape data from Indeed.co.uk using BS4 and Selenium; Extract key info using regex; plot data using Seaborn; carry out statistical tests (Point Biserial Coef.); Use LDA to look for latent topics in job descriptions.
### **Data** 
Webscrapped job descriptions from Indeed.co.uk, searched for on the morning of 20th November, 2020. 500 Jobs originally stored. 2 were found to be unusable / duplicated. Thus I have 498 job descriptions, of which 243 state any kind of salary.
### **Analysis** 

![states_salary](https://github.com/Ioana-P/Analysing_developer_jobs/blob/master/fig/percent_jobs_state_salary.jpg)

Fig 1 - how many jobs do state a salary?

1. Just over half of SE jobs do **not** advertise salary openly. 


![dist_all](https://github.com/Ioana-P/Analysing_developer_jobs/blob/master/fig/distribution_annual.jpg)
Fig 2 - distribution of salaries across the board


![dist_ldn](https://github.com/Ioana-P/Analysing_developer_jobs/blob/master/fig/distribution_annual_London.jpg)
Fig 3 - distribution of salaries for London

2. The median job salary is £45k. The London median is 58K (mean of ~ 60k).

![locations](https://github.com/Ioana-P/Analysing_developer_jobs/blob/master/fig/top_10_locs.jpg)
Fig 4 - number of jobs by location

3. Twice as many posted jobs are non-London than based in the capital. These jobs are however extremely spread out amongst many different locations. Cambridge, Reading, Birmingham and Oxford are the following cities in terms of number of jobs posted.
    
![title_ngrams](https://github.com/Ioana-P/Analysing_developer_jobs/blob/master/fig/title_uni_and_bigrams.jpg)
Fig 5 -  terms and bigrams across job titles

4. Less than 1 in 10 jobs are advertising with a programming language directly in their title (e.g. "Python developer"). About 10-20% of roles advertise with level of seniority directly in the title ("senior" vs "junior") and less than 10% directly require a university graduate (at least, going by title). 
    
![prog_langs](https://github.com/Ioana-P/Analysing_developer_jobs/blob/master/fig/programming_languages.jpg)
Fig 6 - top programming languages

5. The 3 languages in greatest demand (both in terms of overall, total frequency - i.e. counting two mentions in one post as two - as single mentions) are JavaScript (and variants such as CoffeeScript and TypeScript), Python and Java. 

    ### Was there any association between any of the top programming languages and salary?
    With an $\alpha$ of 0.05 (corrected to 0.01 for proposed number of statistical tests), I set out to test if mentions of certain programming languages correlated with salaries. Tested for outliers, normality and equal variance amongst subgroups. Calculated Point Biserial Coefficient. Failed to reject null hypothesis for any programming language group. 
    
    >Point Biserial Coefficient test results between the dichotomous (mention_Python) var and the continuous (salary) var :
    >P-value     :  0.8696801700715007
    >Correlation :  -0.011201789743642679

    >Point Biserial Coefficient test results between the dichotomous (mention_Java) var and the continuous (salary) var :
    >P-value     :  0.4490789588152162
    >Correlation :  0.051649212912551756

    >Point Biserial Coefficient test results between the dichotomous (mention_JavaScript (or variants)) var and the continuous (salary) var :
    >P-value     :  0.07929926309719958
    >Correlation :  0.11938444648235219

    6. Amongst the few emergent themes, there appear to be the following themes:
    i. Academic / scientific posts - for devs working for research organisations such as Oxford Nanopores Technology or Siemens Digital Industries. 
    ii. Finance - SE roles focussed on building and optimising software for banks and for trading. Think London Stock Exchange (yes, one of their jobs is included here).
    iii. Architecture and computing - SE roles centred around computer architecture or cluster computing - think (Apache) Spark, arm, cluster computing. 
  
  
    
    For topic modelling, detected a few emergent themes (see below and check the pyLDAviz html file).
### **Conclusion** 
    What *can* we infer?
    



To check the topics yourself, copy the URL to the `LDA_viz_plot.html` file in this repository into the field at [this link](https://htmlpreview.github.io/#topic=0&lambda=0.51&term=) and run it (or clone the repo and run locally). I recommend setting the lambda parameter (accessible via the slider in the top-right) to a value between 0.4 and 0.6. 

For a more in-depth explanation of how Latent Dirichlet Allocation works and how to interpret pyLDAviz fully, see [my previous article](https://towardsdatascience.com/latent-dirichlet-allocation-intuition-math-implementation-and-visualisation-63ccb616e094).



References:

* ONS Sector Data - https://www.ons.gov.uk/filters/c60ed96a-df5b-4dbe-bbda-ab407c9639d6/dimensions 
* SlashData Report - 'State of the Developer Nation 19th Edition' - https://slashdata-website-cms.s3.amazonaws.com/sample_reports/y7fzAZ8e5XuKCL1Q.pdf 
* Assumptions of Point Biserial Correlation - https://statistics.laerd.com/spss-tutorials/point-biserial-correlation-using-spss-statistics.php
* Point Biserial Correlation with Python - https://towardsdatascience.com/point-biserial-correlation-with-python-f7cd591bd3b1


Key Assumptions to bear in mind:
* **Data sourcing** - Data was sourced purely from Indeed.co.uk over a limited time span. The individual time of scraping is recorded for each job post inside the raw_data file raw_data/SE_jobs_20_11_2020.csv. Further sampling over time will be needed to replicate or falsify findings.
* **National averages** - ONS data was filtered to retrieve data for 2019 as 2020 data is a. not fully available yet broken down by and b. 2020 survey data was affected by the Covid19 lockdown and the move to telephone polling. Although the 2019 mean salary is not a fair comparison for data retrieved in Q3 2020, it provides a rough benchmark against which we can compare our sample. 
* **Data mining** - The salary extraction method is reliant on the pattern finding of text that "looks like salary data" - i.e. the python script that I wrote searched specifically for text that included "£" followed by any length of numbers (continuous or punctuated by a comma) and a time period phrase such as "per day", "per annum", "a year", etc. Spot-checking showed the method to be robust. Where a range was stated (e.g. "£40,000 - £50,000") the mean was taken. 
* **Webscraping process** - The webscraping tool generally managed to retrieve the maximum of 19 jobs posted per page on Indeed's search result pages. The first part of the scraping had a human-in-the-loop (i.e. myself) monitoring the scraper navigating the page, to ensure data retrieval quality. Occasionally, due to an unforeseen pop-up or a nested html element, I had to scroll the automated Chrome browser in the right direction so that it would carry on retrieving new job post URLs. However, this means that some job posts may have been overlooked. This shouldn't pose a significant problem, since I was sampling from the much larger number of total available job posts, but the sampling method's randomness is reliant on the order in which Indeed presents results. 
* **Searching by title** - 
