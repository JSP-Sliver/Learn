npm install 几种方式以及区别
// 在进行个性化理解之前，我觉得首先熟悉几个概念，作为一个开发人员需要开发的项目肯定不止一个，暂且举例为项目A、项目B，那么每个项目肯定有多个需求进行开发
// 在进行需求开发时，肯定会进行多次开发，暂且命名为开发次数1，开发次数2，开发完成肯定还需要上线，暂且命名为项目上线 --jsp
 
 npm install x -g
 // 安装模块到全局，不会在项目node_modules目录中保存模块包
 // 不会将模块依赖写入devDependencies或dependencies节点
 // 运行npm install初始化项目时不会下载模块
 // 个人理解：此命令会将依赖安装到本电脑到全局环境中，也就是说无论是项目A还是B，只要在此电脑上进行开发，都可以直接获取使用全局依赖，而且此依赖只存在本机上，不会被上传 --jsp


 npm install x
 // 会把x包安装到node_modules目录中
 // 不会修改package.json
 // 之后运行npm install命令时，不会自动安装x
 // 个人理解：此命令适合本次运行项目，例如项目本次调试需要，但是明天开发就不需要了，适合采用此命令进行安装，只会将依赖临时安装到此次项目中，重新在仓库获取代码后依赖消失。删除本地代码后，依赖消失。 --jsp


 npm install x --save
 // 会把x包安装到node_modules目录中
 // 会在package.json的dependencies属性下添加x
 // 之后运行npm install命令时，会自动安装到x到node_modules目录中
 // 之后运行npm install --production或者注明NODE_ENV变量值为production时，会自动安装到msbuild到node_modules目录中，即是在线上环境运行时会将包安装
 // 个人理解：此命令会将依赖安装存储在项目中，是安装到最完整到方式，无论是发布上线，还是本地运行都可以加载到依赖，只需要通过npm i命令初始化，便会获得项目依赖，而且依赖配置也会上传到代码仓库。 --jsp


 npm install x -save-dev
 // 会把x包安装到node_modules目录中
 // 会在package.json的dependencies属性下添加x
 // 之后运行npm install命令时，会自动安装到x到node_modules目录中
 // 之后运行npm install --production或者注明NODE_ENV变量值为production时，不会自动安装x到node_modules目录中
 // 个人理解：此命令与--save的唯一区别就是此命令安装的依赖，当项目上线后依赖会消失，而--save安装的依赖会随着项目上线一直存在必要的配置。 --jsp


 使用原则
 devDependencies节点下的模块是我们在开发时需要的，比如项目中使用的gulp，压缩css、js模块。这些模块在我们项目部署后是不需要的，所以我们可以使用--save-的形式安装。像express这些模块是项目运行时必备的，应该安装在dependencies节点下，所以我们应该使用--save的形式安装。

 总结一句话：运行时需要的包使用--save，否则使用--save-dev