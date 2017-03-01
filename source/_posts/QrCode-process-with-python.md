---
title: 二维码生成和解析工具
date: 2016-06-18
tags: [app, dev, qrcode, python]
categories: [dev, python]
---

QR-Code是用的最多的一种二维码，python环境下生成和解析分别有相应工具包。最近对二维码的生成和解析进行了一些学习，此处仅对qrcode和zbar两个工具包的使用进行介绍。

<!--more-->

## [**qrcode**][1]##
用于生成二维码的工具包。详情参考[qrcode 5.3 : Python Package Index](https://pypi.python.org/pypi/qrcode)，使用起来更简单，如下是示例代码：

### **安装**
```
pip install qrcode
```
### **示例代码**

一般用法
```python
import qrcode 
img = qrcode.make('hello world')
img.save('test.png')
```

高级用法

```python
import qrcode 
qr = qrcode.QRCode(     
    version=1,     
    error_correction=qrcode.constants.ERROR_CORRECT_L,     
    box_size=10,     
    border=4, 
) 
qr.add_data('this is a new qrcode') 
qr.make(fit=True)  
img = qr.make_image()
img.save('test.png')
```

## [**zbar **][2]##
用于解析图像和视频中二维码的工具包。详情参考[ZBar bar code reader](http://zbar.sourceforge.net/index.html)。

### **安装**
由于官方的包最高完美支持到python2.6，而主流python版本用的是2.7，windows下这里有一个2.7的msi，来源不详

### **示例代码**


```
from PIL import Image
import zbar

def get_QR (imgPath):
    scanner = zbar.ImageScanner()
    scanner.parse_config("enable")
    pil = Image.open(imgPath).convert('L')
    width, height = pil.size
    raw = pil.tobytes()
    image = zbar.Image(width, height, 'Y800', raw)
    scanner.scan(image)
    data = ''
    for symbol in image:
        try:
            data += symbol.data.decode('utf-8').encode('sjis').decode('utf-8')
        except:
            data += symbol.data
    del(image)
    if not data:
        data += 'Nan'
    return data

img = 'images/barcode_01.jpg'
qrdata= get_QR(img)
print '[DATA]', qrdata
```

### **中文乱码解决**

由于编码问题（参考：[字符串和编码 - 廖雪峰](http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001386819196283586a37629844456ca7e5a7faa9b94ee8000)），默认unicode编码，所以如果不进行处理，通常会有中文乱码产生，以下为处理方式，经测试ok

```
try:
	data += symbol.data.decode('utf-8').encode('sjis').decode('utf-8')
except:
	data += symbol.data
```

以上简单操作即完成QR-Code的生成和解析工作，不过解析的正确率有待验证，特别是扭曲变形或者背景稍混乱的图片，有可能部分识别错误或者无法识别。

## **Zxing+Zbar**
另外几篇关于Zxing源码的分析，以及Android下整合Zxing和zbar的文章
> 1. [秒杀主流应用的二维码扫描](http://www.lai18.com/content/1012109.html)
> 2. [zxing源码分析——QR码部分](http://kuangjianwei.blog.163.com/blog/static/190088953201361015055110/)
> 3. [zxing源码分析——DataMatrix码部分](http://kuangjianwei.blog.163.com/blog/static/1900889532013612103136888/)

---------

[1]: https://pypi.python.org/pypi/qrcode
[2]: https://pypi.python.org/pypi/zbar
