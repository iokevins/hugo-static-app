---
title: 'Economist Dr. Ray C. Fair''s Vote-Share Equations 2016: Calculating Variable "G", For Non-Academics'
date: 2016-11-05T15:01:00.000-07:00
draft: false
tags: 
- prediction
- fair
- politics
- population
- economics
- gdp
---

### UPDATE:

12/12/2016: as of this writing, Dr. Fair's "VP" prediction, or Democratic share of the two-party presidential vote, versus results:

*   Prediction: 44.0%
*   Result: 

*   Popular vote: 48.07%
*   Electoral college: 43.12%

  

### OVERVIEW

Dr. Ray C. Fair represents the John M. Musser Professor of Economics at Yale University and, since 1978, has published [methods on predicting outcomes of United States elections](https://fairmodel.econ.yale.edu/vote2016/index2.htm), particularly the Presidential race, but also Congress.  
  
A co-worker suggested I review a [May 2015 article](http://www.latimes.com/opinion/op-ed/la-oe-0527-fair-election-prediction-20150527-story.html) on Dr. Fair's 2016 Presidential predictions, which listed four main inputs to the algorithm, all of which I find reasonable:  

1.  Is the President running again?
2.  How long has a party controlled the White House?
3.  Slight but persistent bias in favor of the Republican Party
4.  State of the economy

### PROBLEM STATEMENT

The last factor caught my attention.  

  

Putting my skeptic hat on, I cursorily reviewed the calculations for point four, "State of the economy", I struggled to find detailed steps, for how to find source data, to calculate variable _G_, "growth rate of real per capita GDP in the first three quarters of the on-term election year (annual rate)".  
  
In the various papers I read, Dr. Fair mentions that he retrieved the data via the U.S.Department of Commerce's Bureau of Economic Analysis (BEA) [national income and product accounts (NIPA)](https://en.wikipedia.org/wiki/National_Income_and_Product_Accounts). Unfortunately, in my cursory search, I failed to find specific instructions on how to retrieve the specific NIPA data from the BEA.  

### CALCULATING "G"

Dr. Fair's paper, [Presidential and Congressional Vote-Share Equations](https://fairmodel.econ.yale.edu/RAYFAIR/PDF/2007A.pdf), _American Journal of Political Science_, January 2009, pages 69-70, provides the following calculations:

  

G = \[(Y\_15thQuarter / Y\_12thQuarter) ^ (4/3) − 1\] · 100

  

Y = GDPR / POP

  

GDPR = real GDP (note: chained 2009 dollars \*)

  

POP = population (note: midperiod)

  

\* Quarters increment from the most recent Presidential election cycle. For example, President Obama's second four-year term started in January 2012, so calendar year 2015 has quarters 9, 10, 11, and 12, while calendar year 2016 has quarters 13, 14, 15, and 16. We want quarters 12 and 15, or Q4 2015 and Q3 2016, respectively.

### DATA SOURCES

#### ACCESSING BEA WEB SITE

*   Navigate to [bea.gov](https://www.bea.gov/)
*   Select tab "[National](https://www.bea.gov/national/index.htm)" to access 
*   On screen "National Economic Accounts", in section "Gross Domestic Product (GDP)", select link "Interactive Tables: [GDP and the National Income and Product Account (NIPA) Historical Tables](https://www.bea.gov/iTable/index_nipa.cfm)"
*   On screen "National Data", in section "GDP & Personal Income", select button "[Begin using the data...](https://www.bea.gov/iTable/iTableHTML.cfm?ReqID=9&step=1)"
*   Continue per below

#### **GDPR (GROSS DOMESTIC PRODUCT - REAL)**

*   Follow "Accessing BEA Web Site" notes, above, then proceed
*   Select accordion row "SECTION 1 - DOMESTIC PRODUCT AND INCOME", which expands to reveal a list of tabular reports
*   Select tabular report "[Table 1.1.6. Real Gross Domestic Product, Chained Dollars \[Billions of chained (2009) dollars\] Seasonally adjusted at annual rates](https://www.bea.gov/iTable/iTable.cfm?ReqID=9&step=1#reqid=9&step=3&isuri=1&903=6)"
*   Inspect **Line 1, "Gross domestic product"**, for the desired quarters (for example, year 2016, quarters I, II, and III)
*   Note: Per [Wikipedia](https://en.wikipedia.org/wiki/Chained_dollars), "Chained dollars is a method of adjusting real dollar amounts for inflation over time, so as to allow comparison of figures from different years. Chained dollars generally reflect dollar figures computed with 2009 as the base year."

#### POP (POPULATION)

*   Follow "Accessing BEA Web Site" notes, above, then proceed
*   Select accordion row "SECTION 2 - PERSONAL INCOME AND OUTLAYS", which expands to reveal a list of tabular reports
*   Select tabular report "[Table 2.1. Personal Income and Its Disposition \[Billions of dollars\] Seasonally adjusted at annual rates](https://www.bea.gov/iTable/iTable.cfm?ReqID=9&step=1#reqid=9&step=3&isuri=1&903=58)"
*   Inspect **Line 40, "Population (midperiod, thousands)"**, for the desired quarters (for example, year 2016, quarters I, II, and III)

### EXAMPLE CALCULATION - G, 2016

As of 2016-11-05, the BEA web site lists the following values, per October 28, 2016 revision:

*   GDPR (Billions of chained (2009) dollars, Seasonally adjusted at annual rates)

*   GDPR\_Q12 (Q4 2015): 16,490.7, or 16,490,700,000
*   GDPR\_Q15 (Q3 2016): 16,702.1, or 16,702,100,000

*   Population (midperiod, thousands):

*   POP\_Q12 (Q4 2015): 322,693, or 322,693,000
*   POP\_Q15 (Q3 2016): 324,486, or 324,486,000

*   Y:

*   Y\_Q12 (Q4 2015): GDPR\_Q12 / POP\_Q12

*   16,490,700,000 / 322,693,000 =
*   51.103370696

*   Y\_Q15 (Q3 2016): GDPR\_Q15 / POP\_Q15

*   16,702,100,000 / 324,486,000
*   51.472482634

*   G = \[(Y\_Q15 / Y\_Q12) ^ (4/3) − 1\] · 100

*   Y\_Q12: 51.103370696
*   Y\_Q15: 51.472482634
*   \[( 51.472482634 / 51.103370696 ) ^ (4/3) - 1\] · 100
*   \[( 1.007222849 ) ^ (4/3) - 1\] · 100
*   \[1.00964204 - 1\] · 100
*   \[0.00964204\] · 100
*   0.964204

So, that's how one calculates variable G, "growth rate of real per capita GDP in the first three quarters of the on-term election year (annual rate)", with the latest data.

  

Note: Dr. Fair comes up with a slightly higher G value, of 0.97, so it's possible I'm mistaken, he rounds up, or (?)

### AN ASIDE

Dr. Fair seems to have [donated](https://econ4obama.blogspot.com/2008/04/and-few-more.html) to the Obama presidential campaign, if that matters to you. As Paul Krugman [notes](http://krugman.blogs.nytimes.com/2016/02/19/lack-of-power-corrupts/?_r=0), "I’ve been saying for a while that there are three kinds of economists: liberal professional economists, conservative professional economists, and professional conservative economists. The fourth box is mostly empty, for lack of funding." As a Yale faulty member, Dr. Fair may fall into the first category, what Krugman calls "[saltwater](http://krugman.blogs.nytimes.com/2012/03/05/economics-in-the-crisis/)" economists. Or not. I have no idea.

  

Only noting per my initial skepticism, per my colleague forwarding me articles from conservative publications The Daily Caller and The Los Angeles Times. These publications most likely publicized Dr. Fair's predictions because they supported the conservative narrative, this election cycle.

  

I should also note that Dr. Fair's model does seem to break down, in certain situations. For example, Wikipedia reports 1992 and 2002 seem to represent exceptions. 

  

Dr. Fair, to his credit, notes that while 2016 seems risky for Democrats, based on historical precedent, this risk "could, of course, be trumped by other factors".