交叉编译ceres,首先需要交叉编译eigen和glog
1 交叉编译eigen
由于eigen是include文件,相对好编译,参考https://blog.csdn.net/Zheng_r_w/article/details/107089011
2 glog编译
下载glog源码,切到glog目录下新建一个install的文件夹用来放置lib和include文件,运行./autogen.sh,再运行./configure --prefix=/home/lxd/xiyue/lib/ceres-solver/glog/install --host=aarch64-himix100-linux命令

3 ceres交叉编译
将ceres下面的cmakelists和ceres-solver/internal/ceres下的cmakelists中的关于eigen的部分注释掉,在开头部分添加eigen的路径(include_directories("/home/lxd/xiyue/lib/ceres-solver/eigen/install/include/eigen3") )
建一个build文件夹和放置库文件的install文件夹,并切换到build目录下,进行cmake,报错后双击CMakeCache.txt进入cmake的gui界面配置glog的include和lib的路径以及勾选动态链接库生成,前后点击配置和生成按钮无错误后会生成makefile文件,在终端进行make编译,make install可以在指定的文件夹下面看到生成的交叉编译文件

