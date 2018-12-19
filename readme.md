## 什么是webpack，为什么要使用webapck  
  ***   
#### 导语  
之前一直忙着项目，没时间整理自己的东西，最近刚好发现自己对webpack又如此陌生了，于是整理了一篇关于webpack初探的干货，这里是一点[简单的webpack配置](https://github.com/jiangangzou/webpack-explore/blob/master/1.js)

#### 为什么使用webpck
现今很多网页其实都是可以看做功能丰富的应用，它们拥有着复杂的
javaScript代码和一大堆依赖包。为了简化开发的复杂度，前端社区涌现出很多很好的实践方法    
* 模块化，让我们可以把复杂的文件细小化为小的文件  
* 类似于TypeScript这种在JavaScript基础上拓展的开发语言，使我们能够实现目前的版本javaScript不能直接使用的特性，并且之后还能转换为javaScript文件使浏览器识别
* Scss less等CSS预处理器

这些改进确实大大的提高了我们的开发效率，但在利用他们开发的文件往往需要额外处理才能让浏览器识别，而手动处理又是非常繁琐的，这就为webpack类的工具出现提供了需求
#### 什么是webpack
Webpack可以看做是模块打包机，它做的事情是，分析你的项目结构，找到Javascript模块以及其他的一些浏览器不能直接直接运行的拓展语言，并将其打包成合适的格式以供浏览器使用
##### Webpack和Grunt以及Gulp相比有什么特性
其实Webpack和另外两个并没有太多的可比性，Gulp/Grunt是一种能够优化前端开发流程的 工具，而webpack是一种模块化的解决方案，不过webpack的优点是使得Webpack可以替代Gulp/Grunt工具
Grunt和Gulp的工作方式是：在一个配置文件中，指明对某些文件进行类似编译，组合，压缩等任务的步骤，这个工具之后可以帮你完成
Webpack的工作方式是：把你的项目当做一个整体，通过一个给定的主文件，Wenpack将从这个文件开始找到你的项目的所有依赖文件，使用loader处理他们，最后打包成一个javascript可以识别的文件

webpack处理速度更快更加直接  
#### 开始使用webpack
##### 安装webpack  
webpack可以使用npm安装（最好使用全局安装）
~~~
//全局安装
npm install -g webpack
//局部安装
npm install --save-dev webpack
~~~
##### 正式使用webpack前的准备
1. 在当前文件夹中创建一个package.json文件，这是一个标准的npm说明文件，里面蕴含丰富的信息，包括当前项目的依赖模块，自定义脚本任务等。在终端中使用npm init可以自动创建这个文件
~~~
    npm init
    //输入这个命令后，终端会问你一系列问题。诸如项目名称，项目描述，作者等信息，不过不用担心，如果不准备在npm中发布你的模块，这些问题的答案不重要，默认即可
~~~
 1. package.json文件以及就绪，我们在本项目中安装webpack作为依赖包，
 在根目录下创建两个空文件夹，一个是用来存放我们编写的文件，另外一个是存放webpack打包后的数据，项目目录结构如下所示：  
    ![](./1.png '项目结构')  

- 正确使用webpack
在终端中使用最基础的命令是：
webpack {entry file/入口文件} {denstionation for bundled file/出口文件}
高版本webpack上面命令不适用，为
webpack {entry file/入口文件} {denstionation for bundled file/出口文件}
~~~
webpack data/main.js -o webpack-data/main.bundle.js
~~~
只需要指定一个入口，webpack将会自动识别项目所依赖的文件，当webpack没有进行全局安装时，需要进入到webpack的打包文件夹下进行打包
~~~
node_nodules/.bin
~~~

结果如下：  
    ![](./2.png '打包结果')  
*dist下的文件为项目直接运行文件，如果项目要放到服务器上可以直接把dist文件放上去*

到现在为止webpack已经成功打包好了一个文件了，但是我们会感觉还是很麻烦，请看下文

##### 通过一个配置文件来使用webpack
标题的意思很简单，就是我们能不能使用npm的命令就可以执行我们想要的打包呢。不止如此，而且我们想要webpack更高级的功能（loaders和plugins）也通过一个命令就搞定，既然如此我们为什么不定义一个配置文件呢，我们只要把我们想要做的都放在这里面，然后我们执行命令的时候它自动帮我们搞定了

具体做法：
- 在根目录下新建一个名为webpack.config.js文件，把我们想做的按照规范都放进去，一个简单的配置如下：
~~~
//_dirname是nodejs的一个全局变量指向当前执行脚本所在目录
modules.exports = {
    //webpack的唯一入口文件
    entry: _dirname + "/data/main.js",
    //打包文件存放的位置以及文件名
    output: {
        path:_dirname+"/webpack-data",
        filename: "main.bundle.js"
    }
}
~~~
建好了这个文件，我们要打包文件只需要在终端里面运行webpack就可以了，但是我们不会仅满足于此
于是我们就用npm来引导任务执行，对其进行配置后只需要简单的npm start命令来进行打包。在package.json中对npm脚本部分进行相关设置，方法如下：
~~~
{
    "scripts": {
        "start":"webpack" //相当于把npm的start命令指向webpack命令
    }
}
~~~
注意：package.json的脚本部分已经默认添加了打包启动路径，因此在这里无论是全局或者局部都不需要写详细路径

#### 总结
![](./3.png '关于终端')
这是我终端会输出的信息。很多时候我们只要达到目的了，可能也不会再去管其他的了（虽然我也是这样），但是我较劲了一下，就去查了下输出的信息的意思；
| version | time |
|:--:|:--:|
| webpack版本 | 打包花费的时间 |  

| Asset | Size | Chunks | chunk Names|
|:--:|:--:|:--:|:--:|
| 打包生成的文件 | 打包花的所花时间 | 打包的分块 | 打包的名称 |
还有一个黄色的警告，很明显，也会让我们不是很爽，那让我们再坚持下，赢得最后的胜利
上面我们可以看到，我的webpack版本是4.27.1.那这个问题就迎刃而解了，百度下，webpack4出现这个警告。百度后发现webpack4引入了模式，有三个状态，开发模式-生产模式-无。我们没有设置模式，这样的话我们就可以去我们的那个packjson里面设置下。  

最后简单点，开发模式下代码没有压缩，生产模式下代码压缩了。一直觉得“闻道有先后，术业有专攻，如是而已”，所以在求知路上一直困知勉行，望大佬们指教。
