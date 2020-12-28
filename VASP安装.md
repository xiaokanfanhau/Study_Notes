# VASP安装步骤
## 目录
	1.vmware虚拟机安装
	
	2.centos系统安装
	
	3.Intel Parallel Studio XE 2019编译器安装
	
	4.VASP安装
	
	5.VASP最终测试

## 一. vmware虚拟机安装
#### 1.百度搜索“VM”或者输入网址
	"https://www.vmware.com/cn.html"
[访问VM官网](https://www.vmware.com/cn.html)。
	  
#### 2.下载-产品下载-Workstation Pro(见下图)
![图片](C:\Users\15975\Desktop\makeDown\image\20190921182804841.png)

#### 3.根据自己的系统（Windows），点击相应的安装包下载 
![图片](C:\Users\15975\Desktop\makeDown\image\20190921183145130.png)

#### 4.确定下载的版本，选择立即下载，下载开始，请等待！
![图片](C:\Users\15975\Desktop\makeDown\image\20190921183638880.png)

#### 5.下载完成后，按照安装步骤一步步继续，安装到输入许可证密钥时，可以百度VM15激活码，激活VM。
	"https://blog.csdn.net/qq_43498216/article/details/83591687"
[点此传送](https://blog.csdn.net/qq_43498216/article/details/83591687)
![图片](C:\Users\15975\Desktop\makeDown\image\20190923143310645.png)

## 二. centos系统安装
#### 1.搜索[清华大学开源网站镜像](https://mirrors.tuna.tsinghua.edu.cn/)，站内搜索centos，选择第一个搜索结果。
![图片](new_file_files/1.jpg)
![图片](new_file_files/2.jpg)

#### 2.选择
- 7.8.2003版本 
![图片](new_file_files/3.jpg)
- isos/ 
![图片](new_file_files/4.jpg)
- x86_64/ 
![](new_file_files/5.jpg)
- CentOS-7-x86_64-LiveGNOME-2003.iso，此版本自带桌面图像，不需要再次安装，点击下载系统。
![](new_file_files/6.jpg)
#### 3.打开VM虚拟机 
- 创建新的虚拟机 
![](new_file_files/7.jpg)
- 典型(推荐)
![](new_file_files/8.jpg)
- 选择系统文件，完成安装
![](new_file_files/9.jpg)
#### 4.进入centos系统
- 将系统开机，选择第一条安装centos7

![](C:\Users\15975\Desktop\makeDown\image\20190822105955724.png)
- 直接继续就可以了

![](C:\Users\15975\Desktop\makeDown\image\20190822110127998.png)
- 继续到需要添写ROOT PASSWORD和用户注册，填写信息，以后获取权限和使用WinSCP连接虚拟机会用到。

![](C:\Users\15975\Desktop\makeDown\image\20190822111624521.png)
- 填写完成后进如桌面

![](C:\Users\15975\Desktop\makeDown\image\20190822112958958.png)

## 三. Intel Parallel Studio XE 2019编译器安装
### [安装视频传送](https://www.bilibili.com/video/av39616222/)
#### 1.安装gcc编译器，打开命令窗口，输入su命令和密码获取管理员权限，然后输入
- yum -y install gcc gcc-c++ autoconf pcre pcre-devel make automake
- yum -y install wget httpd-tools vim
- 最后输入gcc --version 检验是否安装成功

![](new_file_files/10.jpg)
#### 2.安装Intel编译器和相关的库
- 将parallel_studio_xe_2019_update1_cluster_edition.tgz包拷贝到Linux里面，通过tar -xzf [文件名]将之解压。
- tar -xzf parallel_studio_xe_2019_update1_cluster_edition.tgz
- 如果当前处于图形环境，就进入此目录，在命令行下运行./install_GUI.sh启动Intel Parallel Studio XE的图形界面的安装程序。
- ./install_GUI.sh
- 启动安装程序之后，按照下面的步骤点击。
![](new_file_files/11.jpg)
![](new_file_files/12.jpg)
![](new_file_files/13.jpg)
- 找到parallel_studio_x.lic的位置
![](new_file_files/14.jpg)
![](new_file_files/15.jpg)
- 选择自定义安装库
![](new_file_files/16.jpg)
![](new_file_files/17.jpg)
![](new_file_files/18.jpg)
- 其中IA32版的组件都不装，因为我们编译程序都是编译64bit版本。要装的组件里只有以下这些是必须的
- ·Intel Fortran Compiler
- ·Intel C++ Compiler
- ·Intel Math Kernel Library 2019 Update 1 for Fortran里的Intel MKL core libraries for Fortran、Fortran 95 interfaces for BLAS and LAPACK、Cluster support for Fortran
- ·Intel Math Kernel Library 2019 Update 1 for C/C++里的Intel MKL core libraries for C/C++、Cluster support for C/C++
- ·Intel MPI Library 2019 Update 1里的Intel MPI Library for applications...
- ·Intel Threading Building Blocks 2019
- 装好后，使用比如gedit ~/.bashrc命令编辑当前用户目录下的.bashrc文件，这里面的内容是每次进入bash终端时自动运行的。
- gedit ~/.bashrc
- 把下面这行加入其中末尾，用来自动配置Intel Parallel Studio XE的运行环境：
- source /opt/intel/parallel_studio_xe_2019/psxevars.sh
![](new_file_files/19.jpg)
- 然后重新进入终端，运行ifort -V，如果显示出了编译器的版本，说明编译器已经可以正常使用了。
- ifort -V
![](new_file_files/20.jpg)
- 然后进入/opt/intel/compilers_and_libraries_2019.1.144/linux/mkl/interfaces/fftw3xf，运行make libintel64命令，过一会儿当前目录下会产生libfftw3xf_intel.a库文件。
- make libintel64
![](new_file_files/21.jpg)
![](new_file_files/22.jpg)
![](new_file_files/23.jpg)
## 四. VASP安装
- 解压VASP包，得到vasp.5.4.4目录。
![](new_file_files/24.jpg)
- 进入此目录，把arch/makefile.include.linux_intel拷到上一级目录下改名为makefile.include，里面的配置专门适合Intel编译器。
![](new_file_files/25.jpg)
- 打开此文件，把其中的OFLAG参数里加入-xhost，这样编译器会使得编译出的程序能够利用当前机子CPU能支持的最高档次的指令集以加速计算，也因此就没必要手动添加其它一些VASP编译教程里诸如-xAVX、-mSSE4.2之类的选项了。
![](new_file_files/26.jpg)
- 之后运行make all命令开始编译。一般半个小时到一个小时可以编译完毕。
![](new_file_files/27.jpg)
- 成功界面
![](new_file_files/30.jpg)
- 编译完成后，在vasp.5.4.4/bin目录下出现了vasp_gam、vasp_ncl、vasp_std三个可执行文件，分别是Gamma only版，非共线版和标准版。为了使用方便，可以把最常用的vasp_std改名为vasp。
- ![](new_file_files/28.jpg)
- 然后在~/.bashrc末尾加入以下这行，使得此目录加入到操作系统寻找可执行文件的路径中：
- export PATH=$PATH:/sob/vasp.5.4.4/bin
![](new_file_files/29.jpg)
![](new_file_files/31.jpg)
- 之后重新进入终端，VASP就可以用了。

## 五. VASP最终测试
- 下载测试[任务包](http://sobereva.com/attach/455/benchmark.Hg.tar.gz)
- http://sobereva.com/attach/455/benchmark.Hg.tar.gz
- 这是个含50个Hg原子的标准测试任务。将之解压，会看到IN-short和IN-long，分别是一个耗时较短和一个耗时较长任务的INCAR文件。
![](new_file_files/32.jpg)
![](new_file_files/33.jpg)
- 这里将IN-short改名为INCAR，进入此目录，输入mpirun -np 4 vasp测试调用四个核心执行此任务。
- mpirun -np 4 vasp
![](new_file_files/34.jpg)
- 然后检查得到的OUTCAR看是否内容正常，没异常的话就说明完全装好了！
![](new_file_files/35.jpg)
![](new_file_files/36.jpg)