#### 环境搭建

##### Anaconda中添加`tensorflow`时报错：

###### [解决办法](https://blog.csdn.net/ling_xiobai/article/details/78659981)

```cmd
//报错信息
CondaHTTPError: HTTP 000 CONNECTION FAILED for url <https://repo.continuum.io/pkgs/main/noarch/repodata.json.bz2>
//解决办法 ① ② ③ ④ 条语句
conda config --add channels https://mirror s.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --set show_channel_urls yes
//最后重新运行即可
conda create -n tensorflow python=3.6
```



###### [添加tensorflow](https://www.cnblogs.com/HongjianChen/p/8385547.html)

###### [安装教程2](https://blog.csdn.net/u013080652/article/details/68922702)

###### [Tensorflow简单安装实用版](https://www.jianshu.com/p/0f2106f5cb31)（成功）

1. 下载安装Anaconda

   1. 安装时勾选仅当前用户&&安装时要添加到环境变量中

   2. 安装成功后管理员打开Anaconda Prompt

   3. conda info --e  来检查当前Anaconda中的环境

   4. 添加清华镜像(可以不添加)

      ```Anaconda prompt
      conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
      
      conda config --set show_channel_urls yes
      ```

      

   5. 添加一个tensorflow环境

      ```Anaconda prompt
      conda create -n tensorflow python=3.6.1
      ```

      

   6. activate tensorflow 开启tensorflow，安装tensorflow(cpu版本)

      ```Anaconda prompt
      pip install --upgrade --ignore-installed tensorflow
      ```

      

   7. Anaconda prompt，开启tensorflow并进入python环境，测试tensorflow是否安装成功

      ```Anaconda prompt
      //python命令行中使用 ;\ 再回车可以输入多行命令
      import tensorflow as tf;\
      
      hello = tf.constant('Hello, TensorFlow!');\
      
      sess = tf.Session();\
      
      print(sess.run(hello))
      ```

      

   8. 成功输出hello则完成安装

2. 下载安装PyCharm

   1. 导入项目文件夹
   2. 设置中为指定项目添加指定的python，选择Anaconda下tensorflow中的python.exe

3. 训练-测试



###### 

