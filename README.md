# 简单计算器
利用 Vue.js 框架制作的一个简单计算器

[演示网站](https://calculator.ret.red)

项目编号 HW-004

## 说明

1. 要先**点击答案区域使其获得焦点**才能采用键盘输入。此时右上角会出现“KEYBOARD ON”字样。按键如下表。

| 功能  | 按键                         |
|------|-----------------------------|
| C/AC | `c` / `C`                   |
| +/-  | `~ (shift+&#0060;)`         |
| %    | `% (shift+5)`               |
| +    | `+` / `NUM+`                |
| -    | `-` / `NUM-`                |
| ×    | `* (shift+8)` / `NUM*`      |
| ÷    | `/` / `NUM/`                |
| =    | `Enter` / `NUM Enter` / `=` |
| 0~9  | `0`~`9` / `NUM0`~`NUM9`     |
| .    | `.` / `NUM.`                |

2. 清除按一下是清除当步，再按一下是清除全部。

3. 在 Chrome/Edge 浏览器中测试通过，在 IE 中无法正常显示，Safari 未测试。

4. 经测试，在屏幕宽度极小（小于7寸）的情况下会出现轻微的按键显示错位。与屏幕宽度有关而与窗口大小无关，原因不明。

5. 对于浮点数计算的精度问题，我自创了一个方法进行解决。不确定是不是最优解决方法。

6. 为了不损失数据，我允许显示数据长度超出显示框范围。

7. 代码风格依照 ESLint Standard 进行修正。

8. 网站在 ubuntu 18.04 + node 10.7.0 + npm 6.1.0 环境下反复安装测试通过。

## 运行方法

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

更多信息请参阅 [指引](http://vuejs-templates.github.io/webpack/) 和 [vue-loader 文档](http://vuejs.github.io/vue-loader)。
