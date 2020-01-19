## Online shopping price log

**Project description:** When I was after a pair of black shoes I created this simple script to track the daily price.

```python
from bs4 import BeautifulSoup as soup
from urllib.request import urlopen as uReq
import datetime
from time import sleep



filename = "clarks_tracking.csv"
f = open(filename, "w")
headers = "date, price\n"
f.write(headers)
f.close()
url = "https://www.clarks.co.uk/c/Truxton-Plain/p/26121997"
f = open(filename,"a")

try:
	while True:
		f = open(filename,"a")
		date = str(datetime.date.today())
		uClient = uReq(url)
		page_html = uClient.read()
		uClient.close()
	
		page_soup = soup(page_html, "html.parser")
		price = page_soup.findAll("span", {"class":"product-price-span"})
		for i in price:
		    f.write(date + "," + str(i.text.strip()) + "\n")
		f.close()
		sleep(86400)
except KeyboardInterrupt:
	f.close()
```