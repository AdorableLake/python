```python
#Downloading And Scraping The Contents Of A Web Page
##We Download the contents of the web page:
url = "http://www.ibm.com"

##We use get to download the contents of the webpage in text format and store in a variable called data:
data  = requests.get(url).text 

##We create a BeautifulSoup object using the BeautifulSoup constructor
soup = BeautifulSoup(data,"html5lib")  # create a soup object using the variable 'data'

##Scrape all links
for link in soup.find_all('a',href=True):  # in html anchor/link is represented by the tag <a>
    print(link.get('href'))

##Scrape all images Tags
for link in soup.find_all('img'):# in html image is represented by the tag <img>
    print(link)
    print(link.get('src'))
    
    
##Scrape data from HTML tables

#The below url contains an html table with data about colors and color codes.
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DA0321EN-SkillsNetwork/labs/datasets/HTMLColorCodes.html"
Before proceeding to scrape a web site, you need to examine the contents, and the way data is organized on the website. Open the above url in your browser and check how many rows and columns are there in the color table.

#get the contents of the webpage in text format and store in a variable called data
data  = requests.get(url).text
soup = BeautifulSoup(data,"html5lib")

#find a html table in the web page
table = soup.find('table') # in html table is represented by the tag <table>

#Get all rows from the table
for row in table.find_all('tr'): # in html table row is represented by the tag <tr>
    # Get all columns in each row.
    cols = row.find_all('td') # in html a column is represented by the tag <td>
    color_name = cols[2].string # store the value in column 3 as color_name
    color_code = cols[3].string # store the value in column 4 as color_code
    print("{}--->{}".format(color_name,color_code))
    
#Scrape data from HTML tables into a DataFrame using BeautifulSoup and Pandas
import pandas as pd

##The below url contains html tables with data about world population.
url = "https://en.wikipedia.org/wiki/World_population"
Before proceeding to scrape a web site, you need to examine the contents, and the way data is organized on the website. Open the above url in your browser and check the tables on the webpage.

##get the contents of the webpage in text format and store in a variable called data
data  = requests.get(url).text
soup = BeautifulSoup(data,"html5lib")

##find all html tables in the web page
tables = soup.find_all('table') # in html table is represented by the tag <table>

##we can see how many tables were found by checking the length of the tables list
len(tables)

##Assume that we are looking for the 10 most densly populated countries table, we can look through the tables list and find the right one we are look for based on the data in each table or we can search for the table name if it is in the table but this option might not always work.
for index,table in enumerate(tables):
    if ("10 most densely populated countries" in str(table)):
        table_index = index
print(table_index)

##See if you can locate the table name of the table, 10 most densly populated countries, below.
print(tables[table_index].prettify())
population_data = pd.DataFrame(columns=["Rank", "Country", "Population", "Area", "Density"])
​
for row in tables[table_index].tbody.find_all("tr"):
    col = row.find_all("td")
    if (col != []):
        rank = col[0].text
        country = col[1].text
        population = col[2].text.strip()
        area = col[3].text.strip()
        density = col[4].text.strip()
        population_data = population_data.append({"Rank":rank, "Country":country, "Population":population, "Area":area, "Density":density}, ignore_index=True)
​
population_data

#Scrape data from HTML tables into a DataFrame using BeautifulSoup and read_html
##Using the same url, data, soup, and tables object as in the last section we can use the read_html function to create a DataFrame.
##Remember the table we need is located in tables[table_index]

##We can now use the pandas function read_html and give it the string version of the table as well as the flavor which is the parsing engine bs4.
pd.read_html(str(tables[5]), flavor='bs4')

##The function read_html always returns a list of DataFrames so we must pick the one we want out of the list.
population_data_read_html = pd.read_html(str(tables[5]), flavor='bs4')[0]
population_data_read_html

#Scrape data from HTML tables into a DataFrame using read_html
##We can also use the read_html function to directly get DataFrames from a url.
dataframe_list = pd.read_html(url, flavor='bs4')

##We can see there are 25 DataFrames just like when we used find_all on the soup object.
len(dataframe_list)

##Finally we can pick the DataFrame we need out of the list.
dataframe_list[5]

##We can also use the match parameter to select the specific table we want. If the table contains a string matching the text it will be read.
pd.read_html(url, match="10 most densely populated countries", flavor='bs4')[0]    

```

Authors: Ramesh Sannareddy

Other Contributors: Rav Ahuja

2020-10-17	0.1	Joseph Santarcangelo Created initial version of the lab	

Copyright © 2020 IBM Corporation. 

This notebook and its source code are released under the terms of the MIT License.
