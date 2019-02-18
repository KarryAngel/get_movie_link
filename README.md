# get_movie_link
#电影天堂下载链接
import requests
from bs4 import BeautifulSoup
from urllib.request import quote
#quote()函数，可以帮我们把内容转为标准的url格式，作为网址的一部分打开

movie_name=input('请输入您想要看的电影：')
url_part=quote(movie_name.encode('gbk'))
url='http://s.ygdy8.com/plus/so.php?typeid=1&keyword='+url_part
headers={'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/72.0.3626.109 Safari/537.36'}

res=requests.get(url,headers=headers)
res.encoding='gb2312'
print('状态码：{}'.format(res.status_code))
soup=BeautifulSoup(res.text,'html.parser')
tables=soup.find_all('table')
for table in tables[1:]:
    link=table.find('a')['href']
    movie_link='https://www.ygdy8.com'+link
    movie_name_search=table.find('a').text
    print('电影名:{movie_name_search}\n电影下载链接:{movie_link}\n'.format(movie_name_search=movie_name_search,movie_link=movie_link))
