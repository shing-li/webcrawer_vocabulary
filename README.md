首先下載最新版本python
再到命令提示字元執行以下指令：

easy_install pip
pip install openpyxl
pip install jupyter notebook
pip install requests
pip install beautifulsoup4

下面為程式碼：

import requests
from bs4 import BeautifulSoup
from openpyxl import load_workbook

wb1 = load_workbook('test.xlsx')	#開檔讀excel
f = open('explanations.txt','a')	#開檔寫txt
ws1 = wb1.active 

#f.write('\n')

for k in range(3063,3146):
    content = ws1.cell(row=k, column=1)

    r = requests.get("https://www.thefreedictionary.com/"+content.value) 
    soup = BeautifulSoup(r.text,'html.parser') 
    sel = soup.find(class_ = 'ds-list')
    
    print(sel.text)
    f.write(sel.text)
    f.write('\n')
    
f.close()

參考文章：
https://buzzorange.com/techorange/2017/08/04/python-scraping/
https://ithelp.ithome.com.tw/articles/10202121
https://www.itread01.com/articles/1498941489.html
https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/365164/