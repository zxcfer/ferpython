---
layout: post
title: "Selenium Async"
tags: ["selenium", "async"]
---

# Extract after loading

```py
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.common.exceptions import TimeoutException
from pyvirtualdisplay import Display

def getElementValue(driver, search_type, css_class):
  try:
    element = WebDriverWait(driver, 10).until(EC.presence_of_element_located((search_type, css_class)) )
    # element = WebDriverWait(driver, 10).until(EC.visibility_of_element_located((By.CLASS_NAME, cssclass)) )
    if element.text:
      return element.text
    else:
      return None
  except TimeoutException:
    print "Selenium timeout for <"+css_class+">"
  finally:
    pass

display = Display(visible=0, size=(1024, 768))
display.start()

driver = webdriver.Firefox()
driver.get('https://www.google.com/search?q=rowe+digital')
twitter = getElementValue(driver, By.CLASS_NAME, '_ksh') #_ksh
wikipedia = getElementValue(driver, By.CLASS_NAME, 'kno-ecr-pt')
sitelinks = getElementValue(driver, By.CSS_SELECTOR, 'table.nrgt')
```