```python
!pip install bs4
!pip install requests
```

    Defaulting to user installation because normal site-packages is not writeable
    Collecting bs4
      Downloading bs4-0.0.1.tar.gz (1.1 kB)
      Preparing metadata (setup.py): started
      Preparing metadata (setup.py): finished with status 'done'
    Requirement already satisfied: beautifulsoup4 in c:\programdata\anaconda3\lib\site-packages (from bs4) (4.11.1)
    Requirement already satisfied: soupsieve>1.2 in c:\programdata\anaconda3\lib\site-packages (from beautifulsoup4->bs4) (2.3.1)
    Building wheels for collected packages: bs4
      Building wheel for bs4 (setup.py): started
      Building wheel for bs4 (setup.py): finished with status 'done'
      Created wheel for bs4: filename=bs4-0.0.1-py3-none-any.whl size=1257 sha256=d281098cb9a2c31e7156dd8ef29de38e984514151ea1ee024744892f7372ef48
      Stored in directory: c:\users\ebuka\appdata\local\pip\cache\wheels\73\2b\cb\099980278a0c9a3e57ff1a89875ec07bfa0b6fcbebb9a8cad3
    Successfully built bs4
    Installing collected packages: bs4
    Successfully installed bs4-0.0.1
    Defaulting to user installation because normal site-packages is not writeable
    Requirement already satisfied: requests in c:\programdata\anaconda3\lib\site-packages (2.28.1)
    Requirement already satisfied: charset-normalizer<3,>=2 in c:\programdata\anaconda3\lib\site-packages (from requests) (2.0.4)
    Requirement already satisfied: urllib3<1.27,>=1.21.1 in c:\programdata\anaconda3\lib\site-packages (from requests) (1.26.11)
    Requirement already satisfied: certifi>=2017.4.17 in c:\programdata\anaconda3\lib\site-packages (from requests) (2022.9.14)
    Requirement already satisfied: idna<4,>=2.5 in c:\programdata\anaconda3\lib\site-packages (from requests) (3.3)
    


```python
from bs4 import BeautifulSoup
import requests
```


```python
import requests
import pandas as pd
from bs4 import BeautifulSoup

# URL of the Wikipedia page you want to scrape
url ="https://en.wikipedia.org"

# Send a GET request to the URL
response = requests.get(url)
content = response.content

# Parse the content using Beautiful Soup
soup = BeautifulSoup(content, "html.parser")

# Find all header tags (h1, h2, h3, h4, h5, h6)
header_tags = soup.find_all(["h1", "h2", "h3", "h4", "h5", "h6"])

# Extract text from header tags and store in a list
header_texts = [tag.get_text() for tag in header_tags]

# Create a DataFrame using Pandas
data = {"Header": header_texts}
df = pd.DataFrame(data)

# Display the DataFrame
print(df)

```

                              Header
    0                      Main Page
    1           Welcome to Wikipedia
    2  From today's featured article
    3               Did you know ...
    4                    In the news
    5                    On this day
    6       Today's featured picture
    7       Other areas of Wikipedia
    8    Wikipedia's sister projects
    9            Wikipedia languages
    


```python
import requests
import pandas as pd
from bs4 import BeautifulSoup

# URL of the page with the list of former presidents
url = "https://presidentofindia.nic.in/former-presidents.htm"

# Send a GET request to the URL
response = requests.get(url)
content = response.content

# Parse the content using Beautiful Soup
soup = BeautifulSoup(content, "html.parser")

# Find the table containing the list of former presidents
table = soup.find("table", {"class": "tablepress tablepress-id-8"})

# Initialize lists to store president names and their respective terms
president_names = []
president_terms = []

# Iterate through rows of the table to extract data
for row in table.find_all("tr")[1:]:  # Skip the header row
    columns = row.find_all("td")
    if len(columns) >= 2:
        name = columns[0].get_text()
        term = columns[1].get_text()
        president_names.append(name)
        president_terms.append(term)

# Create a DataFrame using Pandas
data = {"Name": president_names, "Term of Office": president_terms}
df = pd.DataFrame(data)

# Display the DataFrame
print(df)


```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    ~\AppData\Local\Temp\ipykernel_9228\2830917070.py in <module>
         21 
         22 # Iterate through rows of the table to extract data
    ---> 23 for row in table.find_all("tr")[1:]:  # Skip the header row
         24     columns = row.find_all("td")
         25     if len(columns) >= 2:
    

    AttributeError: 'NoneType' object has no attribute 'find_all'



```python
import requests
import pandas as pd
from bs4 import BeautifulSoup

# Function to scrape and create a data frame
def scrape_and_create_dataframe(url, headers, columns):
    response = requests.get(url, headers=headers)
    content = response.content
    soup = BeautifulSoup(content, "html.parser")
    
    table = soup.find("table", {"class": "table rankings-table"})
    data_rows = table.find_all("tr", {"class": "table-body"})

    data_list = []

    for row in data_rows:
        columns_data = row.find_all("td")
        data_list.append([column.get_text().strip() for column in columns_data])

    df = pd.DataFrame(data_list, columns=columns)
    return df

# URL and headers
base_url = "https://www.icc-cricket.com/rankings/mens/team-rankings/odi"
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
}

# Scrape and create data frames
teams_url = f"{base_url}"
teams_columns = ["Position", "Team", "Matches", "Points", "Rating"]
teams_df = scrape_and_create_dataframe(teams_url, headers, teams_columns)

batsmen_url = f"{base_url}/batsmen"
batsmen_columns = ["Position", "Player", "Team", "Rating"]
batsmen_df = scrape_and_create_dataframe(batsmen_url, headers, batsmen_columns)

bowlers_url = f"{base_url}/bowlers"
bowlers_columns = ["Position", "Player", "Team", "Rating"]
bowlers_df = scrape_and_create_dataframe(bowlers_url, headers, bowlers_columns)

# Display data frames
print("Top 10 ODI Teams:")
print(teams_df.head(10))
print("\nTop 10 ODI Batsmen:")
print(batsmen_df.head(10))
print("\nTop 10 ODI Bowlers:")
print(bowlers_df.head(10))

```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    ~\AppData\Local\Temp\ipykernel_9228\369598031.py in <module>
         30 teams_url = f"{base_url}"
         31 teams_columns = ["Position", "Team", "Matches", "Points", "Rating"]
    ---> 32 teams_df = scrape_and_create_dataframe(teams_url, headers, teams_columns)
         33 
         34 batsmen_url = f"{base_url}/batsmen"
    

    ~\AppData\Local\Temp\ipykernel_9228\369598031.py in scrape_and_create_dataframe(url, headers, columns)
         10 
         11     table = soup.find("table", {"class": "table rankings-table"})
    ---> 12     data_rows = table.find_all("tr", {"class": "table-body"})
         13 
         14     data_list = []
    

    AttributeError: 'NoneType' object has no attribute 'find_all'



```python
import requests
import pandas as pd
from bs4 import BeautifulSoup

# Function to scrape and create a data frame
def scrape_and_create_dataframe(url, headers, columns):
    response = requests.get(url, headers=headers)
    content = response.content
    soup = BeautifulSoup(content, "html.parser")
    
    table = soup.find("table", {"class": "table rankings-table"})
    data_rows = table.find_all("tr", {"class": "table-body"})

    data_list = []

    for row in data_rows:
        columns_data = row.find_all("td")
        data_list.append([column.get_text().strip() for column in columns_data])

    df = pd.DataFrame(data_list, columns=columns)
    return df

# URL and headers
base_url = "https://www.icc-cricket.com/rankings/womens/team-rankings/odi"
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
}

# Scrape and create data frames
teams_url = f"{base_url}"
teams_columns = ["Position", "Team", "Matches", "Points", "Rating"]
teams_df = scrape_and_create_dataframe(teams_url, headers, teams_columns)

batters_url = f"{base_url}/batting"
batters_columns = ["Position", "Player", "Team", "Rating"]
batters_df = scrape_and_create_dataframe(batters_url, headers, batters_columns)

allrounders_url = f"{base_url}/all-rounder"
allrounders_columns = ["Position", "Player", "Team", "Rating"]
allrounders_df = scrape_and_create_dataframe(allrounders_url, headers, allrounders_columns)

# Display data frames
print("Top 10 Women's ODI Teams:")
print(teams_df.head(10))
print("\nTop 10 Women's ODI Batters:")
print(batters_df.head(10))
print("\nTop 10 Women's ODI All-rounders:")
print(allrounders_df.head(10))

```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    ~\AppData\Local\Temp\ipykernel_9228\1759925695.py in <module>
         30 teams_url = f"{base_url}"
         31 teams_columns = ["Position", "Team", "Matches", "Points", "Rating"]
    ---> 32 teams_df = scrape_and_create_dataframe(teams_url, headers, teams_columns)
         33 
         34 batters_url = f"{base_url}/batting"
    

    ~\AppData\Local\Temp\ipykernel_9228\1759925695.py in scrape_and_create_dataframe(url, headers, columns)
         10 
         11     table = soup.find("table", {"class": "table rankings-table"})
    ---> 12     data_rows = table.find_all("tr", {"class": "table-body"})
         13 
         14     data_list = []
    

    AttributeError: 'NoneType' object has no attribute 'find_all'



```python
import requests
import pandas as pd
from bs4 import BeautifulSoup

# Function to scrape and create a data frame
def scrape_and_create_dataframe(url, headers):
    response = requests.get(url, headers=headers)
    content = response.content
    soup = BeautifulSoup(content, "html.parser")
    
    articles = soup.find_all("div", {"class": "Card-titleContainer"})
    
    data_list = []

    for article in articles:
        headline = article.find("h3").get_text().strip()
        time = article.find("time").get_text().strip()
        news_link = article.find("a")["href"]
        data_list.append([headline, time, news_link])

    df = pd.DataFrame(data_list, columns=["Headline", "Time", "News Link"])
    return df

# URL and headers
url = "https://www.cnbc.com/world/?region=world"
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
}

# Scrape and create data frame
news_df = scrape_and_create_dataframe(url, headers)

# Display the data frame
print(news_df)

```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    ~\AppData\Local\Temp\ipykernel_9228\3729311429.py in <module>
         29 
         30 # Scrape and create data frame
    ---> 31 news_df = scrape_and_create_dataframe(url, headers)
         32 
         33 # Display the data frame
    

    ~\AppData\Local\Temp\ipykernel_9228\3729311429.py in scrape_and_create_dataframe(url, headers)
         14 
         15     for article in articles:
    ---> 16         headline = article.find("h3").get_text().strip()
         17         time = article.find("time").get_text().strip()
         18         news_link = article.find("a")["href"]
    

    AttributeError: 'NoneType' object has no attribute 'get_text'



```python
import requests
import pandas as pd
from bs4 import BeautifulSoup

# Function to scrape and create a data frame
def scrape_and_create_dataframe(url, headers):
    response = requests.get(url, headers=headers)
    content = response.content
    soup = BeautifulSoup(content, "html.parser")
    
    articles = soup.find_all("div", {"class": "pod-listing"})
    
    data_list = []

    for article in articles:
        paper_title = article.find("h2").get_text().strip()
        authors = article.find("div", {"class": "Authors"}).get_text().strip()
        published_date = article.find("span", {"class": "published-online"}).get_text().strip()
        paper_url = article.find("a")["href"]
        data_list.append([paper_title, authors, published_date, paper_url])

    df = pd.DataFrame(data_list, columns=["Paper Title", "Authors", "Published Date", "Paper URL"])
    return df

# URL and headers
url = "https://www.journals.elsevier.com/artificial-intelligence/most-downloaded-articles"
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
}

# Scrape and create data frame
articles_df = scrape_and_create_dataframe(url, headers)

# Display the data frame
print(articles_df)

```

    Empty DataFrame
    Columns: [Paper Title, Authors, Published Date, Paper URL]
    Index: []
    


```python
import requests
import pandas as pd
from bs4 import BeautifulSoup

# Function to scrape and create a data frame
def scrape_and_create_dataframe(url, headers):
    response = requests.get(url, headers=headers)
    content = response.content
    soup = BeautifulSoup(content, "html.parser")
    
    restaurant_containers = soup.find_all("div", {"class": "restaurant-container"})
    
    data_list = []

    for restaurant in restaurant_containers:
        name = restaurant.find("div", {"class": "restnt-info"}).find("h4").get_text().strip()
        cuisine = restaurant.find("div", {"class": "restnt-info"}).find("p", {"class": "double-line-ellipsis"}).get_text().strip()
        data_list.append([name, cuisine])

    df = pd.DataFrame(data_list, columns=["Restaurant Name", "Cuisine"])
    return df

# URL and headers
url = "https://www.dineout.co.in/bangalore-restaurants"
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
}

# Scrape and create data frame
restaurants_df = scrape_and_create_dataframe(url, headers)

# Display the data frame
print(restaurants_df)

```

    Empty DataFrame
    Columns: [Restaurant Name, Cuisine]
    Index: []
    


```python

```
