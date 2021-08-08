# openCV-nodejs 学习

openCV主要是图像识别相关的，我们这里使用nodejs去使用openCV



#### 一、基础准备

1、opencv4nodejs调用包的地址：

https://www.npmjs.com/package/opencv4nodejs

2、opencv4nodejs文档地址

https://justadudewhohacks.github.io/opencv4nodejs/docs/Mat/#bgrToGray



#### 二、环境安装

##### 方法一：

1、不要先安装opencv4nodejs

cnpm install --save opencv4nodejs 结果下载半天，cpu狂飙，最后测试还是出错。这是因为opencv4nodejs默认帮你下载opencv，结果node_modules一大包快1G了，容易出问题，很烦的。

所以这样做：

1. 安装 Homebrew

2. 安装 Cakebrew 界面版homebrew

    https%3A//cakebrew-377a.kxcdn.com/cakebrew-1.2.5.dmg

3. 安装 opencv

4. 安装 opencv4nodejs（设置变量关闭自动下载）

5. 测试效果

2、设置环境变量

export OPENCV4NODEJS_DISABLE_AUTOBUILD=1

brew install cmake
brew unlink tesseract
Export OPENCV4NODEJS_DISABLE_AUTOBUILD=1
sudo npm install -g node-gyp
brew link opencv
brew install opencv
brew link tesseract

##### 方法二：

  因为使用brew安装opencv会安装到brew下面的文件夹例如："/opt/homebrew/Cellar/opencv/4.5.3_2/include"，但是opencv4nodejs使用的openCV是在/user/local/下面的。如果使用brew安装的这里就需要进行ln -s 软连接。要不就会报错

 1、 这里面我们使用方法二进行安装 首先我们去官网下载资源包https://opencv.org/releases/

 2、使用brew install cmake 安装cmake

3、进到步骤一下载的解压包里面 创建文件夹build。mkdir build

4、配置文件

`cd build`
`cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local ..`

5、进行编译安装

`make -j6＃并行运行6个作业`
`sudo make install`

安装好 OpenCV 后，在 /usr/local/lib 下能看到这样的文件这说明已经安装成功了

然后就可以安装opencv4nodejs。

export OPENCV4NODEJS_DISABLE_AUTOBUILD=1 （这个命令主要是方式安装opencv4nodejs包的时候在安装opencv在/node_modules/opencv-build里面，如果先通过这种方法安装就 cd ./node_modules/opencv-build  node install.js）



```js
npm install --save opencv4nodejs
```



#### 三、遇到的问题

##### 错误一

info install OPENCV_LIB_DIR is not set, looking for default lib dir
info install using lib dir: /usr/local/lib
/Users/hanxiang1/工作相关/github_study/appium-test/node_modules/opencv4nodejs/install/install.js:45
  throw new Error('no OpenCV libraries found in lib dir: ' + libDir)
  ^

Error: no OpenCV libraries found in lib dir: /usr/local/lib

//方法一 ：指定homebrew安装的opencv位置

  `"dependencies": {`
    `"opencv4nodejs": "^5.6.0",`

  `},`
  `"opencv4nodejs": {`
    `"disableAutoBuild": 1,`
    `"opencvIncludeDir": "/opt/homebrew/Cellar/opencv/4.5.3_2/include",`
    `"opencvLibDir": "/opt/homebrew/Cellar/opencv/4.5.3_2/lib",`
    `"opencvBinDir": "/opt/homebrew/Cellar/opencv/4.5.3_2/bin"`
  `}`

 方法二：（ps：网上看见的 但是没用过）
 Step 1 : Find the opencv lib location on your mac using this below command

find / -name "OpenCVConfig.cmake"
Step 2 : Gives you the below path

/opt/homebrew/Cellar/opencv/4.5.2_4/lib
Step 3 : Open zshrc file

open ~/.zshrc 
Step 4 : Place the below line in zshrc file
export OPENCV_LIB_DIR="/opt/homebrew/Cellar/opencv/4.5.3_2/lib"
Step 5 : Save & Close the zshrc file 
Step 6 : Execute below command
source ~/.zshrc 
Step 7 : Now try to do npm i opencv4nodejs

