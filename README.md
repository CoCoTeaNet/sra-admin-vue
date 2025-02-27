# SraAdmin-Vue

## 预备环境
以下是SraAdmin服务端：
1. SraAdmin（springboot3版本）：https://github.com/CoCoTeaNet/sra-admin
2. SraAdmin-Solon（solon版本）：https://github.com/CoCoTeaNet/sra-admin-solon

## Project setup（安装依赖）
```
yarn install
```

### Compiles and hot-reloads for development（开发调试）
```
yarn dev
```

### Compiles and minifies for production（项目打包）
```
yarn build
```

### Customize configuration
See [Configuration Reference](https://vitejs.cn/vite3-cn/config/).

### 或者使用fnm
```shell
# 配置 fnm 环境
fnm env --use-on-cd | Out-String | Invoke-Expression
# 下载并安装 Node.js
fnm use --install-if-missing 20
# 使用yarn
corepack enable yarn
yarn install
yarn dev
```
