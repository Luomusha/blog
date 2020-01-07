# package.json中依赖整合

## 概括
现代工程化的前端项目，总离不开构建工具，依赖管理工具等。
构建工具现代常见的有webpack、rollup、parcel等。
依赖管理工具有npm、yarn等。

今天我们梳理一下package.json中，npm以及yarn中的依赖管理。

## 包添加

### 公共库添加

* 普通添加

```bash
yarn add vue
npm install vue
```

* 按照版本添加

```bash
yarn add vue@2.6.10
npm install vue@2.6.10
```

* 按照tag添加

```bash
yarn add vue@v2.6.10
npm install vue@v2.6.10
```

### 私有库添加

* git私有仓库添加

```bash
yarn add git@10.0.0.9:zhuchuanpeng/example_repo.git
yarn add http://10.0.0.9:9005/zhuchuanpeng/example_repo.git

npm install git@10.0.0.9:zhuchuanpeng/example_repo.git
npm install http://10.0.0.9:9005/zhuchuanpeng/example_repo.git
```

* git私有仓库按照branch添加

```bash
yarn add git@10.0.0.9:zhuchuanpeng/example_repo.git#dev
yarn add http://10.0.0.9:9005/zhuchuanpeng/example_repo.git#dev

npm install git@10.0.0.9:zhuchuanpeng/example_repo.git#dev
npm install http://10.0.0.9:9005/zhuchuanpeng/example_repo.git#dev
```


* git私有仓库按照tag添加
注意这种房的tag，好像不支持“.”字符。比如release_1.0.1这种tag会报错

```bash
yarn add git@10.0.0.9:zhuchuanpeng/example_repo.git#example_tag
yarn add http://10.0.0.9:9005/zhuchuanpeng/example_repo.git#example_tag

npm install git@10.0.0.9:zhuchuanpeng/example_repo.git#example_tag
npm install git+ssh://cloud@172.16.71.3:chuanpeng1.zhu/fr-circle-css-component.git
npm install http://10.0.0.9:9005/zhuchuanpeng/example_repo.git#example_tag
```

* git私有仓库使用access token添加

这种仅限于http方式

```bash
yarn add http://oauth:exampletokentokentoken@10.0.0.9:9005/zhuchuanpeng/example_repo.git
npm install http://oauth:exampletokentokentoken@10.0.0.9:9005/zhuchuanpeng/example_repo.git
```

