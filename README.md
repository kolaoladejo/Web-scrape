import xlsxwriter
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager

element_list = []


for page in range(1, 3, 1):
    
    page_url = "https://www.amazon.{country}/dp/{asin}" + str(page)
    driver = webdriver.Chrome(ChromeDriverManager().install())
    driver.get(page_url)

    title = driver.find_elements_by_class_name("titles")
    image_URL = driver.find_elements_by_class_name("image_URLs")
    price = driver.find_elements_by_class_name("prices")
    detail = driver.find_elements_by_class_name("tdetails")

  
    for i in range(len(title)):
        element_list.append([title[i].text, image[i].text, price[i].text, details[i].text])
  
with xlsxwriter.Workbook('amazonscraping.xlsx') as workbook:
    worksheet = workbook.add_worksheet()
  
    for row_num, data in enumerate(element_list):
        worksheet.write_row(row_num, 0, data)
  
driver.close()
