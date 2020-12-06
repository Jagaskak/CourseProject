# README
This folder contains the IEM and NY Times data from May-Oct 2000

## IEM Data
The data was collected from the Iowa Electronic Markets 2000 U.S. Presidential Election: Winner-Takes-All Market
- https://iemweb.biz.uiowa.edu/closed/pres00_WTA.html
- https://iemweb.biz.uiowa.edu/pricehistory/pricehistory_SelectContract.cfm?market_ID=29

## NY Times Data
The preferred dataset would be to use the LDC corpus. Since we do not have access, we decided to scrape the data ourselves. The code to scrape the data can be found in NYTimesScraper.py
### Setup developer account and create API key
To run the script, you will need to setup a free developer account on NYTimes.
1. Go to https://developer.nytimes.com/apis and create an account
2. When you login, click your profile (email) and in the dropdown you will see a tab called "Apps"
3. Click on "+ New App"
4. Fill out the Overview information, choose the Archive API, and click Create
### How to run the script
1. Copy the API Key that is generated in the procedure above
2. Create a new file locally and copy the API key to it (Make sure you don't push it to your repo later)
3. Edit line 6 in the code to the name of the file where you stored your key
4. Run script
### Disclaimers/Warnings
- Because there are +12k for all 6 months we are looking at (+15k in Oct), I went ahead with the processing step of only keeping paragraphs that mention Gore or Bush. If you'd like to keep all the data, comment out the part where I search for "Gore" or "Bush"
- It takes 2+ hours to gather data for one month (so be prepared to wait a while)
- If you're printing out the contents of the API call, your computer may freeze. Don't panic, just wait about 30 seconds.
- There were several broken links to articles when I was scraping the articles. These articles may be in the LDC corpus, but since we don't have access, I don't know for sure. These articles may or may not be important, but hopefully, since we have a lot of data, the missing articles are negligible
### Data Format
Since we only need the date and the article content, the format is kept very simple. Every line in the txt files corresponds to one article. Every line is formatted as ```<date>,<content>```. Only split on the first ```,``` you see.
