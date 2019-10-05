本文参考了 https://blog.csdn.net/u012491646/article/details/79688979

小白写的日记帖，欢迎指导。

直接使用mac的terminal进python，想导入一个中文分词的包 jieba。导入成功后，可以通过 pip list 查看包已导入。但是进入到JupyterLab后，仍然无法 import jieba。
参考了上面的链接后发现，JupyterLab使用的环境和机器的python环境好像并不是一个，JupyterLab的包在另一个地方。在terminal的python里输入

```
import sys
sys.path
```

可以看到机器的路径是在

```
>>> import sys
>>> sys.path
['', '/Library/Python/2.7/site-packages/pip-19.2.3-py2.7.egg', '/Library/Python/2.7/site-packages/jieba-0.39-py2.7.egg', '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python27.zip', '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7', '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/plat-darwin', '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/plat-mac', '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/plat-mac/lib-scriptpackages', '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/lib-tk', '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/lib-old', '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/lib-dynload', '/Library/Python/2.7/site-packages', '/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python', '/System/Library/Frameworks/Python.framework/Versions/2.7/Extras/lib/python/PyObjC']
```

而在JupyterLab里输入同样的代码，得到的路径是

```
['/Users/pudding/Documents/程序文稿/python',
 '/Users/pudding/anaconda3/lib/python37.zip',
 '/Users/pudding/anaconda3/lib/python3.7',
 '/Users/pudding/anaconda3/lib/python3.7/lib-dynload',
 '',
 '/Users/pudding/anaconda3/lib/python3.7/site-packages',
 '/Users/pudding/anaconda3/lib/python3.7/site-packages/aeosa',
 '/Users/pudding/anaconda3/lib/python3.7/site-packages/IPython/extensions',
 '/Users/pudding/.ipython']
```

可以看到真的不太一样。

接着在terminal里照葫芦画瓢输入命令，进入JupyterLab路径下的bin目录，安装包：

```
➜  ~ cd /Users/pudding/anaconda3/bin
➜  bin ./pip install package
Collecting package
  Using cached https://files.pythonhosted.org/packages/27/16/89ea913b3e70256b9abe4f222543553fcce8bafc7ff3774a8802a054e6b8/package-0.1.1.tar.gz
    Complete output from command python setup.py egg_info:
    Traceback (most recent call last):
      File "<string>", line 1, in <module>
      File "/private/var/folders/wc/fjh7t_7571qb1ttnkqdy3vh40000gn/T/pip-install-9p11pkhx/package/setup.py", line 31
        """
          ^
    SyntaxError: invalid syntax
    
    ----------------------------------------
Command "python setup.py egg_info" failed with error code 1 in /private/var/folders/wc/fjh7t_7571qb1ttnkqdy3vh40000gn/T/pip-install-9p11pkhx/package/
```

我觉得我是理解错了，参考链接里人家写 pip install package 中的 package 是要我替换成我要装的package名字，哎，无奈语文不好。再一次尝试：

```
➜  bin ./pip install jieba
Collecting jieba
  Downloading https://files.pythonhosted.org/packages/71/46/c6f9179f73b818d5827202ad1c4a94e371a29473b7f043b736b4dab6b8cd/jieba-0.39.zip (7.3MB)
    100% |████████████████████████████████| 7.3MB 23kB/s 
Building wheels for collected packages: jieba
  Building wheel for jieba (setup.py) ... done
  Stored in directory: /Users/pudding/Library/Caches/pip/wheels/c9/c7/63/a9ec0322ccc7c365fd51e475942a82395807186e94f0522243
Successfully built jieba
Installing collected packages: jieba
Successfully installed jieba-0.39
```

这一次好像成功了。在JupyterLab里可以成功导入jieba包。

不过我还有一些不明白的地方：

在finder里进入 /Users/pudding/anaconda3/bin 后，并没有找到 jieba 安装在哪里的。难道是安装在

```
/Users/pudding/Library/Caches/pip/wheels/c9/c7/63/a9ec0322ccc7c365fd51e475942a82395807186e94f0522243
```

里面？应该不是，这只是存放临时文件的地方。留个坑吧，以后再填。



