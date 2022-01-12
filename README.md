## 1. ESLint

[`ESLint`](https://eslint.org/)是运行代码分析并分析潜在错误的程序。它是高度可配置的，具有各种内置选项，可以与各团队的风格指南相匹配。当开发者在编辑器中输入代码时，`ESLint`可以突出显示错误，并在编辑器控制台中显示错误的逐项列表。

## 2. Prettier

`Prettier`是当前最流行的代码格式化程序，支持多种语言并与大多数代码编辑器集成，支持开发者设置个人的偏好，例如：制表符的宽度、尾随逗号、括号间距等。

也许开发者不能写出最好看的、最规范的代码，但是借助于`Prettier`，开发者可以不用花费太多的精力在这上面。待猛烈敲击键盘后，保存文件时，`Prettier`可以自动地帮助开发者格式化代码。

## 3. VSCode 集成 Prettier + ESLint + Airbnb 风格指南

该步骤的目的在于：

1. 基于定义的`ESLint`规则，将`Prettier`设置为主要的代码格式化工具；
2. 禁用`ESLint`中的所有格式化规则，只是将它用来抛出错误，并让`Prettier`格式化代码；
3. 配置`VSCode`，使得在保存文件时自动调用`Prettier`按照定义的`ESLint`规则格式化代码。

### 3.1 环境准备

在开始之前，需要确保你的计算机已经安装如下内容：

1. `Visual Studio Code`，并安装`ESLint`和`Prettier`扩展；
2. 安装`Node`环境；
3. `Node`环境安装`ESLint`和`Prettier`相关扩展；
   - 安装`ESLint`：`npm install eslint --save-dev`
   - 安装`Prettier`：`npm install prettier --save-dev`
4. 创建一个空的文件夹，作为本步骤的示例文件夹；
5. 初始化`package.json`：`npm init`

### 3.2 初始化 ESLint 配置并集成 Airbnb 配置

使用命令`eslint --init`初始化`ESLint`配置，其中：

- `How would you like to define a style for your project?`步骤，依次选择`Use a popular style guide`、`Airbnb`；
- `What format do you want your config file to be in?`步骤，选择`JSON`。

### 3.3 配置 Prettier

1. 依次安装`eslint-config-prettier`和`eslint-plugin-prettier`

   - 安装命令：`npm install -D eslint-config-prettier eslint-plugin-prettier`；
   - `eslint-config-prettier`：禁用`ESLint`的格式化，并关闭所有不必要或者可能与`Prettier`冲突的规则；
   - `eslint-plugin-prettier`：将`Prettier`作为`ESLint`规则运行，并将差异报告为单个`ESLint`问题。

2. 修改`.eslintrc.json`，修改内容如下：

   - 在`"extends"`中追加`"prettier"`
   - 增加`"plugins": ["prettier"],`
   - 在`"rules"`中追加`"prettier/perttier": ["error"]`

   修改后的`.eslintrc.json`文件内容如下：

   ```json
   {
     "env": {
       "browser": true,
       "es2021": true
     },
     "extends": ["airbnb-base", "prettier"],
     "plugins": ["prettier"],
     "parserOptions": {
       "ecmaVersion": 12,
       "sourceType": "module"
     },
     "rules": {
       "prettier/perttier": ["error"]
     }
   }
   ```

3. 创建`.prettierrc`文件，存储相关的格式化设置，以下提供了一些简单示例：

   ```json
   {
     "printWidth": 100,
     "singleQuote": true
   }
   ```

### 3.4 配置 VSCode

1. 在项目文件夹中创建文件夹`.vscode`；

2. 在`.vscode`文件夹中创建`settings.json`，并配置如下内容：

   ```json
   {
     "editor.defaultFormatter": "esbenp.prettier-vscode",
     "[javascript]": {
       "editor.defaultFormatter": "esbenp.prettier-vscode"
     },
     "editor.tabSize": 2,
     "editor.formatOnSave": true
   }
   ```
