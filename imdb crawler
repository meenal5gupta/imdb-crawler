
import sys

import requests
import bs4
import csv
from urllib.parse import urljoin
import unicodedata
def crawler():
        arr=["http://www.imdb.com/title/tt0111161/?pf_rd_m=A2FGELUUNOQJNL&pf_rd_p=2398042102&pf_rd_r=07XG6QFJZEE6BBVY6J2Z&pf_rd_s=center-1&pf_rd_t=15506&pf_rd_i=top&ref_=chttp_tt_1"]
        fp=open('data.csv',"w")
        a=csv.writer(fp,delimiter=',',quotechar="$")
        visited=[]
        c=0
        while c<200:
            page=arr.pop()
            if page not in visited: 
                r=requests.get(page)
                soup=bs4.BeautifulSoup(r.text)
                rate=unicodedata.normalize('NFKD',soup.find("span",attrs={"itemprop":"ratingValue"}).string).encode('ascii','ignore')
                n=float(rate)
                if n>6.5 and n<=8.5:
                    c=c+1
                    name=unicodedata.normalize('NFKD',soup.find("h1",attrs={"itemprop":"name"}).text).encode('ascii','ignore')
                    year=soup.find(attrs={"id":"titleYear"}).text
                    director=unicodedata.normalize('NFKD',soup.find("span",attrs={"itemprop":"name"}).string).encode('ascii','ignore')
                    print([c,name,year,director,n])
                    a.writerow([c,name,year,director,n])
                divs=soup.find_all('div',attrs={"class":"rec-title"})
                links=[div.find('a')['href'] for div in divs]
                links=[urljoin(page,link) for link in links]
                arr=list(set(arr)|set(links))
                visited.append(page)
        fp.close()
crawler()

