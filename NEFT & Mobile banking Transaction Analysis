##first import necessary libraries and modules

import pandas as pd
import requests
from bs4  import *
import numpy as np

--------------------------------------------NEFT Transaction Analysis after scraping data-------------------------------------------

##create soup first: #this involves web scraping of data and tables from the given url. Here basically function is defined to
## to save time and increase functionality.

def create_soup(url,payload=None,parser='lxml'):
    page = requests.get(url,params=payload)         #this makes request for data from given url
    if page.status_code==200:                       #if output shows 200 that means connection with site is succesful
        soup = BeautifulSoup(page.text,parser)       # data is fetched from site.
        print("Enjoy the soup!!")
        return soup
    else:
        print("Website is invalid!! Respose code is {}.".format(page.status_code))
        
        


## Create soup for month of by using given url.
url= 'https://www.rbi.org.in/Scripts/NEFTUserView.aspx?Id=132'
april_soup = create_soup(url)


##here we are fetching the required table from the web page. attrs(attributes) are given after inspecting site and HTML tags 
april_table_neft= april_soup.find_all('table', attrs={'width':'95%'})
#find_all gives list



### now getting data from list of tags instead of tags
for i in april_table_neft:   #here first we have to find tr from list and then proceed similarly as in first case.
    tt= i.find_all('tr')
    april_table_neftlist = []
    for k in tt:
        temp= []
        tdd = k.find_all('td')
        for j in tdd:
            data = j.get_text()
            #print(j.get_text(), end= ' ')
            temp.append(data)
        print('\n\n')
        april_table_neftlist.append(temp)
        
        
 
## Getting dataframe from the above list:
dfapril= pd.DataFrame(april_table_neftlist[2:293])   #do slicing only after inspecting the rows of the table and the values inside table

###Similarly make dataframe for months of January, Febraury and March


## After getting data , concat all months data into single dataframe:
#CREATING SINGLE DATAFRAME and assigning columns name

columns=['Banks', 'NO. OF OUTWARD TRANSACTIONS', 'outward AMOUNT (Rs. Million)', 'NO. OF INWARD TRANSACTIONS','INWARD AMOUNT (Rs. Million)','month']
datas= pd.concat([df_jan,df_feb, df_march,dframe_april], ignore_index= True)
datas.columns= columns
datas


#inspecting data
datas.info()


##changing column types so that graph and data analysis can be done.
datas['NO. OF OUTWARD TRANSACTIONS']=pd.to_numeric(datas['NO. OF OUTWARD TRANSACTIONS']) 
datas['outward AMOUNT (Rs. Million)']=pd.to_numeric(datas['outward AMOUNT (Rs. Million)']) 
datas['NO. OF INWARD TRANSACTIONS']=pd.to_numeric(datas['NO. OF INWARD TRANSACTIONS']) 
datas['INWARD AMOUNT (Rs. Million)']=pd.to_numeric(datas['INWARD AMOUNT (Rs. Million)']) 


----------Fews questions--------
### sorting banks in terms of maximun no of outward transactions:
datas.groupby('Banks').sum().sort_values(by='NO. OF OUTWARD TRANSACTIONS', ascending = False).head()

output of above :
NO. OF OUTWARD TRANSACTIONS	outward AMOUNT (Rs. Million)	NO. OF INWARD TRANSACTIONS	INWARD AMOUNT (Rs. Million)
Banks				
HDFC BANK	119513496	12381857.39	64782330	11768396.16
STATE BANK OF INDIA	95811245	12259111.41	197027440	13684412.20
RBI,PAD	92315985	7248387.30	5409229	1480101.63
AXIS BANK	74048129	5551629.86	38653995	5066052.14
ICICI BANK LTD	72470015	5507653.71	50259558	6777117.53
#####

#drawing subplots for top five banks where z5 represents top 5 banks interms of total transacations
z5.plot(kind='box', rot= '90')

## drwing bar plots for five banks.  
df.head().plot(kind='bar', x= 'bankname')

NOTE:  After analysing data, it is found that State Bank of India is followed by HDFC bank in terms of most number of transactions, total amount of transactions. There is huge gap after these banks for the bank at 3rd position.



-----------------------------------Mobile Transaction (after scraping data from given url) Analysis Below-------------------------------------------------

#Steps are similar till finding table from web page

#for month of January , data is scraped and converted intp dataframe . You can do similarly for other months

urljan= 'https://www.rbi.org.in/Scripts/NEFTUserView.aspx?Id=129'
soup_jan= create_soup(urljan)
mobiletransactionstablejan= soup_jan.find_all('table', attrs={'width':'85%'})

## now getting data from list of tags instead of tags
for i in mobiletransactionstablejan:   #here first we have to find tr from list and then proceed similarly as in first case.
    tt= i.find_all('tr')
    mobiletransactionlistjan = []
    for k in tt:
        temp= []
        tdd = k.find_all('td')
        for j in tdd:
            data = j.get_text()
            #print(j.get_text(), end= ' ')
            temp.append(data)
        print('\n\n')
        mobiletransactionlistjan.append(temp)
        
        
#dataframe from list:
dfjan= pd.DataFrame(mobiletransactionlistjan[2:243])


#after fetching data for all months:
df= pd.concat([dfjan, dffeb, dfmarch, dfapril], ignore_index= True)
df.head()

#drawing bar grapgh for for first five banks:
df.head().plot(kind='bar', x= 'bankname')



##THANK YOU for reading this. 



