# wepy 项目初始化

* 安装 wepy 脚手架工具

  npm install wepy-cli -g

* 查看安装的版本

  wepy --version

* 使用 wepy 命令初始化项目

  wepy init standard my-project # 初始化一个标准的项目
  wepy init empty pyg_30 # 初始化一个空的项目

* 进入项目目录

  cd pyg_30

* 安装依赖包

  npm install
  yarn

* 启动项目

  yarn dev

* 项目的原理

  我们在 src/wpy 文件中写代码,最终会打包成 dist 文件夹中

* 在微信开发者工具中打开 dist 目录（最终的小程序的代码）

  vscode 的作用： 写小程序代码的微信开发者工具的作用： 预览效果以及调错

# 使用 git 管理项目

* 初始化仓库

```bash
git init
```

* 添加代码

```bash
git add .
```

* 提交代码

```bash
git commit -m '初始化提交'
```

* 去 github 创建一个仓库（必须是一个空的仓库）
* 添加别名

```bash
git remote add origin git@github.com:hucongcong/pyg_30.git
```

* 推送代码到远程仓库

```bash
git push -u origin master
```

# 项目的目录说明

```
1. dist: 最终的打包目录
2. 依赖包
3. src: 开发目录
4. .editorconfig: 统一编辑器的配置， 依赖vscode的插件  editorconfig
5. .eslintrc: eslint的配置文件
6. .gitignore: git的忽视文件
7. .prettierrc： 这是prettier的配置文件，配合prettier插件,如果项目中有这个prettierrc文件，优先级比默认配置要高
```

# wepy 项目的微信开发者工具的配置

1.  关闭微信开发者工具中， es6 转 es5
2.  关闭微信开发者工具中，上传代码自动补全
3.  关闭微信开发者工具中，上传代码自动压缩
4.  开启 不校验合法域名

# wepy 文件高亮问题

1.  默认 vscode 打开 wpy 文件不会高亮的
2.  安装`vetur`插件（已经装好了）
3.  点击 wpy 文件右下角，找到纯文本
4.  选择`.wpy文件`的配置关联
5.  选择 vue 进行关联
6.  以后 wpy 文件的高亮都是 vue 的高亮了

也可以直接在配置文件中

```js
    // 文件关联
    "files.associations": {
      "*.vue": "vue",
      "*.wpy": "vue"
    }
```

# wpy 文件编译的说明

```
1. style -----> wxss
2. template ------> wxml
3. script(除了config) ------> js
4. script中的config --------> json
```

# 项目的 app.json 的基本配置

## pages

1.  需要在 pages 中增加新的页面

```js
pages: ['pages/index', 'pages/category', 'pages/cart', 'pages/my'];
```

2.  在 pages 中新建对应的文件

## window

```js
window: {
      navigationBarBackgroundColor: '#ff2d4a',
      navigationBarTitleText: '优购',
      navigationBarTextStyle: 'white'
    },
```

## tabBar

```js
tabBar: {
      selectedColor: '#ff2d4a',
      list: [
        {
          pagePath: 'pages/index',
          text: '首页',
          iconPath: '/assets/images/icon_home@3x.png',
          selectedIconPath: '/assets/images/icon_home_active@3x.png'
        },
        {
          pagePath: 'pages/category',
          text: '分类',
          iconPath: '/assets/images/icon_category@3x.png',
          selectedIconPath: '/assets/images/icon_category_active@3x.png'
        },
        {
          pagePath: 'pages/cart',
          text: '购物车',
          iconPath: '/assets/images/icon_cart@3x.png',
          selectedIconPath: '/assets/images/icon_cart_active@3x.png'
        },
        {
          pagePath: 'pages/my',
          text: '我的',
          iconPath: '/assets/images/icon_me@3x.png',
          selectedIconPath: '/assets/images/icon_me_active@3x.png'
        }
      ]
    }
```

# 首页轮播图的完成

1.  获取轮播图的数据

```
1. 通过wx.request发送ajax请求
2. 把响应数据存储到data里面（注意，在wpy中，数据存储在data中  data={}）
3. 如何修改data中的数据  this.imgList = res.data.data, 如果是同步的代码，不需要同步，如果是异步代码，需要调用$apply()进行同步
```

2.  把数据渲染到轮播图中

# 轮播图中发送 ajax 请求优化说明

1.  wepy 对于小程序中所有的异步方法都进行 promise 的支持
2.  但是需要手动开启 wepy 的 promise 与 async await
3.  如何开启 async 与 await

```
1. 进入项目根目录，安装runtime包  npm install wepy-async-function --save

2. 在app.wpy中引入引入runtime包   import 'wepy-async-function';

3. 在app.wpy中增加
export default class extends wepy.app {

    constructor () {
        super();
        this.use('promisify');
    }

}

4. 以后项目中就可以随意使用async 与 await了
```

# 首页-导航
