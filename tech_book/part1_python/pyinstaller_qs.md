# pyinstaller打包python程序的常见问题

1. **shapely**库相关

   问题：

   ```python
   Unable to find "e:\github\forexe\venv\lib\site-packages\shapely\DLLs\geos.dll" when adding binary and data files.
   ```

   解决：

   在shapely库文件目录下，找到geos_c.dll文件，将其复制一份重命名为geos.dll

   目录：``E:\GitHub\ForExe\venv\Lib\site-packages\shapely\DLLs``![Screenshot_1](https://raw.githubusercontent.com/guangmujun/mybooks/master/tech_book/imgs/Screenshot_1.jpg)

   ![Screenshot_2](https://raw.githubusercontent.com/guangmujun/mybooks/master/tech_book/imgs/Screenshot_2.jpg)

2. **pyproj**库相关

   问题：

   ```python
   ModuleNotFoundError: No module named 'pyproj._datadir'
   ```

   解决：

   pyproj库的安装有问题，到[官网](https://www.lfd.uci.edu/~gohlke/pythonlibs/)  https://www.lfd.uci.edu/~gohlke/pythonlibs/下载对应的包重新安装即可。

   例如我用的window系统64位python3.6,则下载pyproj‑2.1.3‑cp36‑cp36m‑win_amd64.whl到项目文件夹，使用命令

   ``pip install pyproj‑2.1.3‑cp36‑cp36m‑win_amd64.whl ``

   即可正确安装pyproj库

   ![1566438904431](https://raw.githubusercontent.com/guangmujun/mybooks/master/tech_book/imgs/1566438904431.png)

3. **numpy**相关

   问题：

   ```python
   ModuleNotFoundError: No module named 'numpy.random.common'
   ```

   两个解决方法

   方法一：（推荐）

   在打包生成的spec文件中，在hiddenimports参数中添加如下内容：

   ```python
   hiddenimports=['numpy.random.common','numpy.random.bounded_integers','numpy.random.entropy']
   ```

   ![Screenshot_3](https://raw.githubusercontent.com/guangmujun/mybooks/master/tech_book/imgs/Screenshot_3.jpg)

   方法二：

   在使用到numpy库的py文件中，加入下述内容

   ```python
   import numpy.random.common
   import numpy.random.bounded_integers
   import numpy.random.entropy
   ```

4. **sklearn**相关

   问题：

   ```python
   ModuleNotFoundError: No module named 'sklearn.utils._cython_blas'
   ```

   解决:

   在打包生成的spec文件中，在hiddenimports参数中添加如下内容：

   ```python
   hiddenimports=['sklearn.utils._cython_blas','cython', 'sklearn', 'sklearn.ensemble','sklearn.neighbors.typedefs','sklearn.neighbors.quad_tree','sklearn.tree._utils','scipy._lib.messagestream']
   ```

5. **geopandas**库相关

   问题：

   ```python
   File "site-packages\geopandas\datasets\__init__.py", line 7, in <module>
   StopIteration
   [6764] Failed to execute script application
   ```

   解决:

   找到geopandas库文件下的``__init__.py``,将``import geopandas.datasets``这句注释掉



更多内容请见：https://www.guangmujun.cn/