# python_automate_data_layer_audit
This is a project I created in Python to navigate to all pages of a client website, check the values in the data layer, and spit them out into a csv. 

```
driver = webdriver.Chrome()
my_urls = ["https://uat2-aemcs.REDACTED.com/products","https://uat2-aemcs.REDACTED.com/products/door-styles.html","https://uat2-aemcs.REDACTED.com/products/door-styles/macarthur","https://uat2-aemcs.REDACTED.com/products/door-styles/san-mateo","https://uat2-aemcs.REDACTED.com/products/door-styles/portola","https://uat2-aemcs.REDACTED.com/products/door-styles/westerly","https://uat2-aemcs.REDACTED.com/products/door-styles/adelaide","https://uat2-aemcs.REDACTED.com/products/door-styles/garner","https://uat2-aemcs.REDACTED.com/products/door-styles/leesburg","https://uat2-aemcs.REDACTED.com/products/door-styles/glen-ellen","https://uat2-aemcs.REDACTED.com/products/door-styles/brookland","https://uat2-aemcs.REDACTED.com/products/door-styles/savannah","https://uat2-aemcs.REDACTED.com/products/door-styles/shorebrook","https://uat2-aemcs.REDACTED.com/products/door-styles/hanover","https://uat2-aemcs.REDACTED.com/products/door-styles/reading","https://uat2-aemcs.REDACTED.com/products/materials-colors","https://uat2-aemcs.REDACTED.com/products/materials-colors/painted-sage","https://uat2-aemcs.REDACTED.com/products/materials-colors/cherry-amber","https://uat2-aemcs.REDACTED.com/products/materials-colors/cherry-java","https://uat2-aemcs.REDACTED.com/products/materials-colors/duarform-linen","https://uat2-aemcs.REDACTED.com/products/materials-colors/duraform-harbor","https://uat2-aemcs.REDACTED.com/products/materials-colors/duraform-stone","https://uat2-aemcs.REDACTED.com/products/materials-colors/duraform-drift","https://uat2-aemcs.REDACTED.com/products/materials-colors/painted-black","https://uat2-aemcs.REDACTED.com/products/materials-colors/painted-navy","https://uat2-aemcs.REDACTED.com/products/materials-colors/painted-mist","https://uat2-aemcs.REDACTED.com/products/materials-colors/painted-linen","https://uat2-aemcs.REDACTED.com/products/materials-colors/painted-boulder","https://uat2-aemcs.REDACTED.com/products/materials-colors/painted-ember-glaze","https://uat2-aemcs.REDACTED.com/products/materials-colors/painted-harbor","https://uat2-aemcs.REDACTED.com/products/materials-colors/painted-biscotti-glaze","https://uat2-aemcs.REDACTED.com/products/materials-colors/painted-pewter-glaze","https://uat2-aemcs.REDACTED.com/products/materials-colors/painted-vanilla","https://uat2-aemcs.REDACTED.com/products/materials-colors/maple-slate","https://uat2-aemcs.REDACTED.com/products/materials-colors/maple-truffle","https://uat2-aemcs.REDACTED.com/products/materials-colors/maple-cognac","https://uat2-aemcs.REDACTED.com/products/materials-colors/maple-spice","https://uat2-aemcs.REDACTED.com/products/materials-colors/maple-rye","https://uat2-aemcs.REDACTED.com/products/materials-colors/duraform-espresso","https://uat2-aemcs.REDACTED.com/products/materials-colors/duraform-breeze","https://uat2-aemcs.REDACTED.com/products/organization-accents","https://uat2-aemcs.REDACTED.com/products/organization-accents/knobs-pulls-handles","https://uat2-aemcs.REDACTED.com/products/organization-accents/organization","https://uat2-aemcs.REDACTED.com/products/organization-accents/decorative-accessories","https://uat2-aemcs.REDACTED.com/products/organization-accents/range-hoods","https://uat2-aemcs.REDACTED.com/products/how-its-made","https://uat2-aemcs.REDACTED.com/products/catalog","https://uat2-aemcs.REDACTED.com/products/resources","https://uat2-aemcs.REDACTED.com/products/order-samples"]
site_sections = []
sub_sections = []
sub_section_2s = []
page_names = []

for page in my_urls: 
    driver.get(page)
    site_section = driver.execute_script('var myDl = adobeDataLayer.getState(); var myDlKeys = Object.keys(myDl.page); var mySection = myDl.page[myDlKeys[0]]["section"]; return mySection')
    site_sections.append(site_section)
    sub_section = driver.execute_script('var myDl = adobeDataLayer.getState(); var myDlKeys = Object.keys(myDl.page); var mySubSection = myDl.page[myDlKeys[0]]["subSection"]; return mySubSection;')
    sub_sections.append(sub_section)
    sub_section_2= driver.execute_script('var myDl = adobeDataLayer.getState(); var myDlKeys = Object.keys(myDl.page); var mySubSection2 = myDl.page[myDlKeys[0]]["subSection2"]; return mySubSection2;')
    sub_section_2s.append(sub_section_2)
    page_name = driver.execute_script('var myDl = adobeDataLayer.getState(); var myDlKeys = Object.keys(myDl.page); var myPage = myDl.page[myDlKeys[0]]["name"]; return myPage;')
    page_names.append(page_name)
    
dict = {"page_url":my_urls,
       "site_section":site_sections,
       "sub_section":sub_sections,
       "sub_section_2":sub_section_2s,
       "page_name":page_names}

df = pd.DataFrame(dict)

display(df)
```
