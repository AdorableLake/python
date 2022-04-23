————————————————

版权声明：本文为CSDN博主「码农BookSea」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。

原文链接：https://blog.csdn.net/bookssea/article/details/107309591

在以上链接基础做了删改

————————————————

```python
# -*- codeing = utf-8 -*-
from bs4 import BeautifulSoup  # 网页解析，获取数据
import re  # 正则表达式，进行文字匹配`
import urllib.request, urllib.error  # 制定URL，获取网页数据
import xlwt  # 进行excel操作

# 按照高达上海基地限定商品的方式去指定相关规则
# 创建正则表达式
findPic = re.compile(r'<a rel="(.*)">')
findName = re.compile(r'<p>(.*)</p>')
findPrice = re.compile(r'<p>(.*)</p>')
findAge = re.compile(r'<p>(.*)</p>')
findStock = re.compile(r'<p>(.*)</p>')



def main():
    baseurl = "http://lp.gundambase.com.cn/gd/index.php?m=content&c=index&a=lists&catid=43"  #要爬取的网页链接
    # 1.爬取网页
    datalist = getData(baseurl)
    savepath = "高达基地上海限定商品.xls"    #当前目录新建XLS，存储进去
    # dbpath = "gunpla.db"              #当前目录新建数据库，存储进去
    # 3.保存数据
    saveData(datalist,savepath)      

# 爬取网页
def getData(baseurl):
    datalist = []  #用来存储爬取的网页信息
    for i in range(0, 5):  # 调用获取页面信息的函数，5次
        url = baseurl + str(i * 5)
        html = askURL(url)  # 保存获取到的网页源码
        # 2.逐一解析数据
        soup = BeautifulSoup(html, "html.parser")
        for item in soup.find_all('div', class_="item"):  # 查找符合要求的字符串
            data = []  # 保存一款商品所有信息
            item = str(item)
            pic = re.findall(findPic, item)[0]  # 通过正则表达式查找
            data.append(pic)
            name = re.findall(findName, item)[0]
            data.append(name)
            price = re.findall(findPrice, item)[0]
            data.append(price)
            age = re.findall(findAge, item)[0]
            data.append(age)
            stock = re.findall(findStock, item)
            data.append(stock)
            data.append(bd.strip())
            datalist.append(data)

    return datalist


# 得到指定一个URL的网页内容
def askURL(url):
    head = {  # 模拟浏览器头部信息，向豆瓣服务器发送消息
        "User-Agent": "Mozilla / 5.0(Windows NT 10.0; Win64; x64) AppleWebKit / 537.36(KHTML, like Gecko) Chrome / 80.0.3987.122  Safari / 537.36"
    }
    # 用户代理，表示告诉豆瓣服务器，我们是什么类型的机器、浏览器（本质上是告诉浏览器，我们可以接收什么水平的文件内容）

    request = urllib.request.Request(url, headers=head)
    html = ""
    try:
        response = urllib.request.urlopen(request)
        html = response.read().decode("utf-8")
    except urllib.error.URLError as e:
        if hasattr(e, "code"):
            print(e.code)
        if hasattr(e, "reason"):
            print(e.reason)
    return html


# 保存数据到表格
def saveData(datalist,savepath):
    print("save.......")
    book = xlwt.Workbook(encoding="utf-8",style_compression=0) #创建workbook对象
    sheet = book.add_sheet('G-BASE PRODUCTS', cell_overwrite_ok=True) #创建工作表
    col = ("商品名称","图片链接","价格","适用年龄","库存状况")
    for i in range(0,5):
        sheet.write(0,i,col[i])  #列名
    for i in range(0,98):
        # print("第%d条" %(i+1))       #输出语句，用来测试
        data = datalist[i]
        for j in range(0,8):
            sheet.write(i+1,j,data[j])  #数据
    book.save(savepath) #保存

if __name__ == "__main__":  # 当程序执行时
    # 调用函数
     main()
    # init_db("G_base.db")
     print("搞定！")
```
