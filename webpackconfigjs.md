# webpack.config.js

### 多入口，多出口
```
entry:{
    main1:'./src/main1.js',
    main2:''/src/main2.js',
},
output:{
    filename:'[name].js',
    path:path.resolve('dist');
}
```

### babel转义es6 -> es5
```
npm install babel-core --save-dev
npm install babel-loader --save-dev
npm install babel-preset-es2015 --save-dev
```
```javascript
//文件配置
    rules:[
            {
                test:/\.js$/,
                use:'babel-loader',
                exclude:/node_modules/
            },
        ]
//附加.babelrc 文件
    {
        "presets": ["es2015"]
    }

```

### babel转义es7 -> es5
```
npm install babel-preset-stage-0
```
```javascript
//附加.babelrc 文件
    {
        "presets":["es2015","stage-0"]
    }
```

### cssloader
```
npm install css-loader style-loader --save-dev
```
```javascript
//文件配置
    rules:[
            {
                test:/\.css$/,
                use:['style-loader','css-loader']
            }
        ]

```

### less,sass,stylus
```
less-loader less css-loader style-loader
npm install less-loader less css-loader style-loader --save-dev
sass-loader
stylus-loader
```
```javascript
//文件配置
    rules:[
            {
                test:/\.less$/,
                use:['style-loader','css-loader','less-loader']
            }
        ]
```

### 解析图片
```
file-loader
url-loader(依赖于file-loader工作)
```
```javascript
//文件配置
    rules:[
            {
                test:/\.(jpg|png|gif)$/,
                // 8k以下转base64
                use:['url-loader?limit=8192']
            },
        ]
```
```javascript
//js中引入图片的写法
    import page from './before.jpg'
    let  img = new Image();
    //js中引入图片需要写入线上路径，或者使用import
    // img.src = './before.jpg';
    img.src = page;
    document.appendChild(img);
```

### html解析插件
插件的作用是以我们自己的html为模板将打包后的结果，自动引入到html中产生到dist目录
```
npm install html-webpack-plugin --save-dev
```
```javascript
//文件配置
    const htmlWebpackPlugin = require('html-webpack-plugin');
    plugins:[
        new htmlWebpackPlugin({
            template:'src/index.html'
        })
    ]
```

### webpack-dev-server
热更新,启动一个服务
```
npm install webpack-dev-server  --save-dev
```
```javascript
//文件配置
  "scripts": {
    "dev":"webpack-dev-server"
  },
```

### 安装vue-loader vue-template-compiler 
```
vue-loader 解析.vue文件
vue会自动调用vue-template-compiler解析模板

```
```javascript
//loader文件配置
    {
        test:/\.vue$/,
        use:['vue-loader']
    },
// 插件文件配置
    const VueLoaderPlugin = require('vue-loader/lib/plugin')
    plugins:[
        new VueLoaderPlugin()
    ]
```




