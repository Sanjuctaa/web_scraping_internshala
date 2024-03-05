# web_scraping_internshala

## code

### import the libraries

import pandas as pd

import requests

from bs4 import BeautifulSoup

### create empty lists for storing the results

job_title=[]

company=[]

stipend=[]

duration=[]

location=[]

### Scrape the website

for j in range(1,151):

        url='https://internshala.com/internships/page-'+str('j')+str('/')

        page= requests.get(url)
    
        soup= BeautifulSoup(page.text,"lxml")

    
        box= soup.find_all("div", class_="internship_meta")

    for i in box:
    
            j=i.find('h3').text.strip()
            
            job_title.append(j)

    
            c=i.find("div",class_="company_and_premium")
        
            comp=c.find('a').text
        
            co=comp.strip()
        
            company.append(co)
    
    
            internship_details= i.find("div",class_= "individual_internship_details")

    
        
            loc= internship_details.find("div",id_="location_names")
        
            p= internship_details.find("span").text
        
            l= p.strip()
        
            location.append(l)
    
    
            stip= internship_details.find("div",class_="other_detail_item stipend_container")
       
            st= stip.find('div',class_="item_body").text
        
            s= st.strip()
        
            stipend.append(s)

    
            dur= internship_details.find_all("div",class_="other_detail_item")[1]
    
            time=dur.find("div",class_="item_body").text
        
            d=time.strip()
        
            duration.append(d)


  df= pd.DataFrame({'Job Title': job_title,'Company':company,'Location':location, 'Stipend':stipend, 'Duration': duration})
  
  df
    
