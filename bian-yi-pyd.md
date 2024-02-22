# 编译pyd

### python文件类型

* **.py** ：python的源代码文件
* **.pyc** ：Python源代码import后，编译生成的字节码
  * 以pyc 为扩展名的是Python的编译文件。其执行速度快于 py 文件且不能用文本编辑编辑查看。所以 pyc 文件往往代替 py 文件发布。虽然pyc文件加载的速度很快，但很容易被反编译。
* **.pyd** ：Python的动态链接库(Windows平台dll)
  * pyd格式是D语言(C/C++综合进化版本)生成的二进制文件，实际也就是dll文件。该文件目前位置没找到可以被反编译的消息，只能被反汇编。
  * 编译成pyd后，性能会有提升

### py编译成pyd

1.  创建setup.py 文件。如：

    ```python
    from setuptools import setup
    from Cython.Build import cythonize

    setup(
        name='GoogleFanyi1',
        ext_modules=cythonize('GoogleFanyi1.py')
    )

    ```
2.  终端运行命令：

    ```python
     python setup.py build_ext --inplace      
    ```
3. 将生成的pyd文件重命名为py的名字，记住不可更改为其他，否则报错
4. pyd可当作py在代码中导入使用

### pyinataller 打包脚本

* 只可打包py文件
*   代码示例：

    ```python
    pyinstaller PdfFanyi.py --onefile --hidden-import GoogleFanyi1  --hidden-import googletranslate --hidden readme --icon ImprovePdf.ico
    ```
