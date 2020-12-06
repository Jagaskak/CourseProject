# README
This folder contains information about how to collect IEM and NY Times data from May-Oct 2000.

## IEM Data
The data was collected from the Iowa Electronic Markets 2000 U.S. Presidential Election: Winner-Takes-All Market
- https://iemweb.biz.uiowa.edu/closed/pres00_WTA.html
- https://iemweb.biz.uiowa.edu/pricehistory/pricehistory_SelectContract.cfm?market_ID=29

Simply download the data for each month and store as a txt file.

## NY Times Data
The preferred dataset would be to use the LDC corpus. 
If you do not have access, you can scrape the data yourself. We have detailed the steps to do so below. If you do have access, skip to the section "Data Format" below to learn more on how to structure the aggregated data from the LDC corpus.

### Setup developer account and create API key
To run the script, you will need to setup a free developer account on NYTimes.
1. Go to https://developer.nytimes.com/apis and create an account
2. When you login, click your profile (email) and in the dropdown you will see a tab called "Apps"
3. Click on "+ New App"
4. Fill out the Overview information, choose the Archive API, and click Create
### Disclaimers/Warnings
- Because there are +12k for all 6 months of articles that we are looking at (+15k in Oct) and we are only reproducing experiment one in the paper, keep only the paragraphs that mention Gore or Bush. 
- It takes 2+ hours to gather data for one month (so be prepared to wait a while)
- If you're printing out the contents of the API call, your computer may freeze. Don't panic, just wait about 30 seconds.
- There were several broken links to articles when I was scraping the articles. 
### Data Format
Since we only need the date and the article content, the format is kept very simple. Every line in the txt files corresponds to one article. Every line is formatted as ```<date>,<content>```. Only split on the first ```,``` you see.
