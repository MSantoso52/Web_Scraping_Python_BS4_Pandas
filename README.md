# Web_Scraping_Python_BS4_Pandas
Web Scraping Using Python with Beautifulsoup4 &amp; Pandas
# *Overview*
Project repo for data extraction from web using Beautifulsoup4 python library through web scrapping. This repo about step-by-step to conduct web scrapping until convert into CSV file. 
# *Prererquisites*
To follow along this learning need to available the below requirements:
- python3 installed
  ```bash
  sudo apt install python3   
  ```
- pandas library
  ```bash
  pip install pandas   
  ```
- Beautifulsoup
  ```bash
  pip install beautifulsoup4   
  ```
# *Project Flow*
Web scraping process following below process:
1. Import necessary python library
   ```python3
   from bs4 import BeautifulSoup
   import pandas as pd
   import requests
   ```
3. Get response from url
  ```python3
   url = "https://en.wikipedia.org/wiki/List_of_countries_by_GDP_(nominal)"
   ```
5. Fetch the url into Beautifulsoup API as variable
   ```python3
   response = requests.get(url)
   soup = BeautifulSoup(response.content, 'lxml')
   ```
7. Data correction
   ```python3
    # Data correction add 'Nan' after '-'
    for index, i in enumerate(gdp):
    if i == '—':
        gdp.insert(index+1, 'Nan')

   # Data correction '—' replace with 'Nan'
    gdp = list(map(lambda i:'Nan' if i == '—' else i, gdp))
   .....
   # change list shape from 1470x1 to 210x7
   gdp = [gdp[i:i+7] for i in range(0, len(gdp), 7)]
   ```
9. Make data frame
   ```python3
   df = pd.DataFrame(gdp, columns=description)
   ```
11. Convert into csv file
   ```python3
   df.to_csv('World_GDP.csv', index=False)
   ```
