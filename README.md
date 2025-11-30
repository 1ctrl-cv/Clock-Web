# Clock-Web

一个简易的在线时钟

用 vue3 写了这一坨东西来解决学校考试时用的在线时钟有广告的 bug

## 如何部署

- 1、准备一个 Cloudflare 账户
- 2、Fork 本仓库，自由修改`App.vue`和`index.html`文件中的文案
- 3、登录`Cloudflare Dashboard`打开`Workers 和 Pages`创建`Pages`
- 4、`连接到Git`选择`Github`或`Gitlab`中你刚刚Fork的项目，点击开始设置
- 5、只需要修改`框架预设`为`Vue`即可，点击保存并部署，即可部署成功并投入使用

~~*这种东西真的有必要自己部署吗？*~~

## 安装依赖

```sh
npm install
```

### 开发

```sh
npm run dev
```

### 编译生产环境版本

```sh
npm run build
```
