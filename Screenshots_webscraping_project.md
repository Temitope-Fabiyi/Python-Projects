<h1><a name="introduction">Introduction</a></h1>
<p>This project involves web scraping extensive data from the following website: <a class="link" href="<https://ind.nl/en/public-register-recognised-sponsors/public-register-regular-labour-and-highly-skilled-migrants">Public Register of Recognised Sponsors</a>
 The site hosts a list of over 11,000 companies, providing an overview of recognized sponsors for residence purposes, specifically those hiring Regular Labour and Highly Skilled Migrants from various countries. The objective of this project is to extract all the companies listed on the website, conduct a brief Google search for each company, and capture a screenshot of the search results for documentation and analysis purposes.</p>  

 ```python
import os
import time
import random
import requests
from bs4 import BeautifulSoup
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager
import undetected_chromedriver as uc

#Scraping the company's name
url = 'https://ind.nl/en/public-register-recognised-sponsors/public-register-regular-labour-and-highly-skilled-migrants'
response = requests.get(url)
soup = BeautifulSoup(response.content, 'html.parser')

# Selecting all <tr> tags and extracting the first <td> within each <tr>
company_elements = soup.select('tr')
company_names = []

for element in company_elements:
    td_tag = element.find('th')
    if td_tag:
        company_names.append(td_tag.get_text().strip())

#Removing the first element from the list
if company_names:
    del company_names[0]
print(company_names)

len(company_names)

#Creating a directory for screenshots if it doesn't exist
if not os.path.exists('screenshots'):
      os.makedirs('screenshots')

#Setting up Selenium
options = webdriver.ChromeOptions()
options.add_argument('--headless')
# Initializing driver 
#driver = uc.Chrome() 
 
# Try accessing a website with antibot service 
#driver.get("https://nowsecure.nl")
driver = uc.Chrome(service=Service(ChromeDriverManager().install()), options=options)

screenshot_folder = r"C:\Users\USER\Documents\Data Science\Webscraping Project\Screenshots"

# So one of the issues I encountered was the google verification (to confirm if the search was from a robot or human), So in most cases I had to stop the code from running.
# So to know where my screenshot stopped, I created a variable named "start_position"
start_position = 397

# Perform Google search and take screenshots

for company in company_names [start_position:500]:
    driver.get('https://www.google.com')
    search_box = driver.find_element('name', 'q')
    search_box.send_keys(company)
    search_box.send_keys(Keys.RETURN)
    time.sleep(10)  # Wait for the page to load

    #Save the screenshot
    screenshot_path = os.path.join(screenshot_folder,f'{company}.png')
    driver.save_screenshot(screenshot_path)

 
# Initialize the WebDriver
with webdriver.Chrome(service=webdriver_service, options=chrome_options) as driver:
    for url in urls:
        get_screenshot(url, driver, output_dir)
        # Random delay between 5 and 10 seconds before the next request
        time.sleep(10)
        
if (index + 1) % 50 == 0:
    print("Taking a 4-minute break...")
    time.sleep(240)
    
    

# Close the driver
driver.quit()
```  
<p> Using the Python code provided, I successfully achieved the project objective: extracting all the companies listed on the website, conducting a Google search for each company, and capturing screenshots of the search results. Please refer to the <a class="link" href="<https://drive.google.com/drive/folders/1Jh00oCCLAdQAj-RoK0cXwHss1GTWRDg5?usp=drive_link">Link</a> for examples of the screenshots generated from the script. </p>

