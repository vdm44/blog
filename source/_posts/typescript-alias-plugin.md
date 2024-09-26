---
title: typescript-alias-plugin
date: 2024-09-27 03:58:14
tags: typescript
---
# tsc编译时无法转换路径别名的问题
在tsconfig里使用paths来配置路径别名，使用tsc编译之后的文件里没有转换成正确的路径。
可以使用tsc-alias这个包
```
npm install tsc-alias -D
```
需要配合tsc来使用，先用tsc编译，再用tsc-alias来转换路径别名

推荐用concurrently来同时开启tsc和tsc-alias
```
npm install concurrently -D
```
``` json
// package.json
"scripts": {
  "dev": "concurrently \"tsc -w\" \"tsc-alias -w\"",
  "build": "&& concurrently \"tsc\" \"tsc-alias\"",
},
```
``` json
// tsconfig.json
{
  "paths": {
    "@shared/*": ["core/shared/*"]
  }
}
```
``` typescript
// ts文件中使用路径别名导入一个模块
import shared from "@shared/index.ts"
```
