## Ubuntu16.04环境下安装TensorFlow-GPU版

#### 注意事项

---

- 显卡是否支持CUDA

#### 说明

---

- 本次安装的所有操作均是在个人账户下执行的

#### 软件下载

---

- CUDA 9.0：[百度网盘](https://pan.baidu.com/s/1gnu0UmWhdyeSuLxuD852mw) ，提取码为:`2fq2`
- cuDNN 7.1.4：[百度网盘](https://pan.baidu.com/s/1gnu0UmWhdyeSuLxuD852mw) 

#### 安装流程

---

##### 安装显卡驱动 

1. 使用命令`gedit /etc/modprobe.d/blacklist.conf`编辑文件，在文件末尾输入以下内容以屏蔽系统集成显卡驱动：
2. 使用快捷键`Ctrl+Alt+F1`切换至命令行界面；
3. 关闭图形系统：`service lightdm stop`；
4. 删除之前的驱动：`apt purge nvidia-*`；
5. 更新源：`apt update`；
6. 查询驱动的可用版本：`apt-cache search nvidia-*`；
7. 安装驱动：`apt install nvidia-xxx`；**xxx是上一步中查询到可用的最新版本号。**
8. 输入`reboot`命令重启系统。

##### 安装CUDA9.0

1. 下载文件存放于`Download/`目录下；
2. 执行以下命令进行安装：

```
$ dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb
$ apt update
$ apt install cuda
```

3. 输入命令该`gedit ~/.bashrc`编辑文件以配置环境变量，在打开的文件末尾追加以下内容：

```
export CUDA_HOME=/usr/local/cuda
export LD_LIBRARY_PATH=$CUDA_HOME/lib64:$CUDA_HOME/extras/CUPTI/lib64:$LD_LIBRARY_PATH
export PATH=$CUDA_HOME/bin:$PATH
```

4. 输入命令`source /root/.bashrc`使环境变量生效；

5. 输入命令`nvcc -V`查看版本号以验证CUDA是否安装成功

##### 安装cuDNN

1. 下载文件存放于`Download/`目录下；

2. 执行一下命令完成安装：

   法1：

```
tar -zxvf cudnn-9.0-linux-x64-v7.1.tgz
sudo cp cuda/include/cudnn.h /usr/local/cuda/include/
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64/ -d 
sudo chmod a+r /usr/local/cuda/include/cudnn.h
sudo chmod a+r /usr/local/cuda/lib64/libcudnn*
```

​	法2：

```
cd Download/
tar -zxvf ./cudnn-8.0-linux-x64-v6.0.tgz -C $CUDA_HOME/../
```

##### 安装TensorFlow-GPU

使用命名：

`pip3 install tensorflow-gpu==1.x -i https://pypi.tuna.tsinghua.edu.cn/simple `

#### 验证安装

---

1. 启动python命令行：`python3`；
2. 引入tensorflow：`import tensorflow as tf`；
3. 查看tensorflow版本：`tf.__version__`；
4. 创建Session：`tf.Session()`，可以在设备名处看到你的显卡名称表示安装完成；
5. 退出python：`exit()` 
