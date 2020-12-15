开发环境配置
webpack.config.dev.json
```
const { merge } = require('webpack-merge');
const webpack = require('webpack');
const baseConf = require('./webpack.config.base');

module.exports = merge(baseConf, {
    plugins: [
        new webpack.DefinePlugin({
            API_URL: JSON.stringify({
               URL1: "xxxxxxxx",
               URL2: "xxxxxxxxxxx"
            })
        })
    ],
});
```

生产环境配置
webpack.config.prod.json
```
const { merge } = require('webpack-merge');
const webpack = require('webpack');
const baseConf = require('./webpack.config.base');

module.exports = merge(baseConf, {
    plugins: [
        new webpack.DefinePlugin({
            API_URL: JSON.stringify({
               URL1: "ttttttt",
               URL2: "tttttttttttt"
            })
        })
    ],
});
```

package.json文件定义打包命令
```
"build:dev": "set NODE_ENV=development&&webpack --config webpack.config.dev.js --mode development --progress --colors",
"build:prod": "set NODE_ENV=production&&webpack --config webpack.config.prod.js --mode production --progress --colors"
```

然后在控制台输入相应的命令打不同的包
打开发包
```
npm run build:dev
```
打生产包
```
npm run build:prod
```

然后在index.js中引入
```
index: path.resolve(__dirname, 'src/index.js')
```

index.js
```
console.log(API_URL.URL1)
console.log(API_URL.URL2)
```
如果是开发包就会显示
```
xxxxxxxx 
xxxxxxxxxxx
```

如果是生产包就会显示
```
ttttttt
tttttttttttt
```
