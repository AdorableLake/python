```python
# Downloading And Scraping The Contents Of A Web Page

!pip install bs4
# !pip install requests

from bs4 import BeautifulSoup 
# this module helps in web scrapping.

import requests  
# this module helps us to download a web page

url = "http://lp.gundambase.com.cn/gd/index.php?m=content&c=index&a=lists&catid=43"
# We Download the contents of the web page

data  = requests.get(url).text 
# We use get to download the contents of the webpage in text format and store in a variable called data

soup = BeautifulSoup(data,"html5lib")  # create a soup object using the variable 'data'
# We create a BeautifulSoup object using the BeautifulSoup constructor

for link in soup.find_all('a',href=True):  # in html anchor/link is represented by the tag <a>
    print(link.get('href'))
# Scrape all links

for link in soup.find_all('img'):# in html image is represented by the tag <img>
    print(link)
    print(link.get('src'))
# Scrape all images
```
