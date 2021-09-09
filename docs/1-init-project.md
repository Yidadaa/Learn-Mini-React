# 第一节 初始化仓库

为了方便开发，我们使用 [Vite](vitejs.dev) 来作为脚手架工具，使用下面的命令安装并创建一个工程：

```shell
# 在安装前，请确保你已经安装了 yarn
yarn global add vite
yarn create vite learn-mini-react --template vanilla-ts
cd learn-mini-react
yarn
```

我们使用 Vite 的 `vanilla-ts` 模板作为初始项目，该模板会方便我们使用 Typescript 构建后续的模块。

随后，我们在新建的 `learn-mini-react` 基础上进行一些修改，首先我们规整一下目录，将 `html` 入口文件移入 `src`，将 `svg` 文件移动到 `assets` 目录：

```shell
cd learn-mini-react
mv index.html ./src
mkdir ./src/assets
mv ./favicon.svg ./src/assets
```

记得更新 `/src/index.html` 中的 `script` 和 `favicon` 路径：

```html
<!-- line 6: -->
<link rel="icon" type="image/svg+xml" href="./assets/favicon.svg" />
<!-- line: 13 -->
<script type="module" src="./main.ts"></script>
```

然后，我们需要重新配置一下 Vite，使得它能够正确构建我们的项目，在项目根目录新建 `vite.config.js` 文件：

```shell
touch vite.config.js
```

然后填入以下配置：

```js
import { defineConfig } from "vite";

export default defineConfig({
  root: "./src",
  build: {
    outDir: "../dist",
  },
});
```

上述配置文件将 `src` 作为默认构建路径，并修改了 build 产物的输出路径，现在在命令行中测试以下配置是否正确：

```shell
yarn build
```

查看项目根目录是否生成了 `dist` 目录。

然后测试开发模式：

```shell
yarn dev
```

打开 `localhost:3000`，如果看到 `Hello Vite!` 字样，则证明配置正确。

最后，我们开始添加 `mini-react` 模块，在进行下述操作前，请确保你已经在命令行中敲下了 `yarn dev` 命令：

```shell
cd ./src
mkdir mreact
touch ./mreact index.ts
```

在 `/src/mreact/index.ts` 中随便填入一个函数，并在 `/src/main.ts` 中引入它：

```ts
// src/mreact/index.ts
export function sayHello() {
  console.log("hello, mini react");
}

// src/main.ts
import { sayHello } from "./mreact";
sayHello();
```

然后打开 `localhost:3000` 的控制台，看到控制台中能正确输出，则证明我们的脚手架可以正常工作了。
