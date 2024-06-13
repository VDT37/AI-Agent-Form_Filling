# Form Filling AI Agent using Selenium and OpenAI

## Description
This project automates the process of filling out web forms using Selenium and OpenAI's GPT-3.5. It generates user data such as names, addresses, emails, phone numbers, LinkedIn profiles, and conceptual answers for technical questions, then inputs this data into the specified form and submits it.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Features](#features)
- [FAQ](#faq)

## Installation
### Package and library resource requirements
Install the required packages:
```sh
pip install selenium openai webdriver-manager nltk
```
Download the NLTK resources:
```sh
import nltk
nltk.download('punkt')
nltk.download('averaged_perceptron_tagger')
```

## Usage
#### 1. Set up the OpenAI API key:
```sh
import openai
openai.api_key = 'sk-proj-xxxxxxxxxxxxxxxx1zOD'
```
#### 2. Initialize the WebDriver:
```sh
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager

def initialize_webdriver():
    options = webdriver.ChromeOptions()
    options.add_argument('--no-sandbox')
    options.add_argument('--disable-dev-shm-usage')
    options.add_argument('--ignore-certificate-errors')
    options.add_argument('--ignore-ssl-errors=yes')
    driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()), options=options)
    return driver
```
#### 3. Generate Data using OpenAI's GPT-3.5:
```sh
def generate_data(prompt):
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[{"role": "system", "content": "You are a helpful assistant."}, {"role": "user", "content": prompt}]
    )
    return response.choices[0].message['content'].strip()

def generare_field():
    prompt = (
      "Your prompt for the corresponding form field"
    )
    response = generate_data(prompt)
```
#### 4. Fill and Submit the Form:
```sh
def fill_form(driver, form_URL, form_Fields):
    driver.get(form_URL)
    # Add field filling functions here using selenium web scraping methods

def submit_form(driver):
    # code for submit form button
```

#### 5. Run the Main Function:
```sh
def main():
    # Generate the data for each form field using created functions
    first_name, middle_name, last_name = generate_fullname()

    # Assign those variables to their respective form field names
    form_Fields = {
          'First Name' : first_name,
          'Middle Name' : middle_name,
          'Last Name' : last_name
    }

    # Initialize WebDriver
    driver = initialize_webdriver()

    # Fill out and Submit the form
    fill_form(driver, form_URL, form_Fields)
    submit_form(driver)

 
if __name__ == "__main__":
    main()
```

## Features
1. Automatically generates:
   - Full names (first, middle, last)
   - Full addresses
   - Email addresses
   - Phone numbers
   - LinkedIn profile URLs
   - Conceptual answers for technical questions
   - Cover letters
2. Fills out and submits web forms using Selenium WebDriver.


## FAQ
### Q. What are the other approaches to run this task?
**A.** For Web automation, besides Selenium, we can use libraries like:
    - **BeautifulSoup and Requests** for web scraping and interacting with web pages, but not capable of handling dynamic web pages or JavaScript execution, which the specified form incorporates for Resume Upload button.
    - **Scrapy** web scraping framework, which is most oftenly used for scraping exclusively than interacting with forms
    - Other libraries include **Playwright, Puppeteer, and Pyppeteer**

### Q. Why did you choose Selenium approach?
**A.** Although, for better performance in terms of compute cost and modern web feature support, Playwright would be a more efficient alternative, I am more comfortable with selenium than other libraries like Scrapy, Pippeteer/Pyppeteer, and it also meets the project's requirements, making it a sound decision. Moreover, the form appears to have dynamic elements, such as JavaScript and React attributes for its resume upload field, and includes a "Drag and Drop" feature typically found in dynamic forms to enhance user experience. Therefore, 'Selenium' approach, here, is appropriate over the fast and light-weight BeautifulSoup alternative, as Selenium can handle JavaScript-driven interactions and elements that are dynamically displayed or hidden.

    
