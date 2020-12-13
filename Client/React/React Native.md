# * [facebook/react-native](https://github.com/facebook/react-native)

A framework for building native apps with React. http://facebook.github.io/react-native/

* React 是一套可以用简洁的语法高效绘制 DOM 的框架,通过 React 来构建 iOS 原生应用和 Android 原生应用。Virtual DOM 保持不变，你仍然可以使用 JSX 来创建它，但实际的 UI 是用原生的组件构建，
* RN是在Facebook所提出的核心概念Learn once, write anywhere所诞生的产物，着力于提高多平台开发的开发效率。我们可以同时为android和ios两个平台开发App，只需要根据两个平台不一样的地方去做一些调整即可。RN主要负责UI部分，而原生主要负责交互和数据处理。RN属于hybrid开发，并且与原生无缝连接，相比Web App和Native开发，RN取长补短，集合了两者的优势。RN开发的APP可以跳过App Store审核，远程更新代码，提高迭代频率和效率，既有Native的体验，又保留React的开发效率。
* RN的原理是将React代码转化为原生API，iOS一套，Android一套。RN在一开始生成OC模块表，然后把这个模块表传入JS中，JS参照模块表，就能间接调用OC的代码。
* 围绕着React所建立起来的生态系统以及组件化开发思想能有效地分解大规模应用的复杂度、提高资源复用率。拥有以下特性：
  - 同构渲染：服务器端和客户端共用一套代码，一份模板，两端使用。
  - 完全组件化：自动分析加载页面的静态资源依赖。
  - 生态圈：畅享所有 React 组件。
  - 比webview 更好的体验，更好的性能，更好的手机交互
  - 未来发展的一种趋势之一，提前了解学习，装13
  - 解决项目中一些痛点，比如更新，ui方面的需求改动，丰富的运营手段。
* 由于 AppStore 审核周期的限制，如何动态的更改 app 成为了永恒的话题。无论采用何种方式，我们的流程总是可以归结为以下三部曲：“从 Server 获取配置 --> 解析 --> 执行native代码”。
    - 通过 HTTP 请求获取 JSON 格式的配置文件。
    - 配置文件中标记了每一个元素的属性，比如位置，颜色，图片 URL 等。
    - 解析完 JSON 后，我们调用 Objective-C 的代码，完成 UI 控件的渲染。
* React是由Facebook开发出来的用于开发用户交互界面的JS库。其源码由Facebook和社区优秀的程序员维护。React带来了很多新的东西，例如组件化、JSX、虚拟DOM等。其提供的虚拟DOM使得我们渲染组件呈现非常之快，从频繁操作DOM的繁重工作之中解脱。它做的工作更多偏重于MVC中的V层，结合其它如Flux等一起，你可以非常容易构建强大的应用。
* React的世界里，一切都是组件。你可以构建任何直接的HTML没有的组件，例如下拉菜单、导航菜单等。同时，组件里也可以包含其它组件。每一个组件都有一个render方法，用于呈现该组件。同时，每一个组件都有属于自己的scope，从而与其它的组件界定开来，用于构建属于该组件的方法，以方便复用。JSX是基于JS的扩展，它允许你在JS里直接写HTML的代码，而不用像我们过去一样要想在JS里写HTML不得不拼接一大堆的字符串。React不直接操作DOM，频繁的操作DOM会非常影响性能和体验。React将DOM结构储存在内存中，与render方法的返回值进行比较，通过其自由的diff算法计算出不同的地方，然后反应到真实的DOM当中。也就是说，大多数情况我们渲染组件、更改组件状态等都是操作的虚拟DOM，只有在有所改变的情况下，才会反应到真实的DOM当中。React Native基于ReacJS，把 React 编程模式的能力带到移动开发,用来开发iOS和Android原生应用.
* NodeJs 是基于JavaScript的,可以做为后台开发的语言. 提供了很多系统级的API，如文件操作、网络编程等. 用事件驱动, 异步编程,主要是为后台网络服务设计.React Native 借助 Node.js，即 JavaScript 运行时来创建 JavaScript 代码。
* 总结来说，React Native使用NodeJS来做系统处理，使用React来渲染。
* 适用
  - 使用 React Native 从头开始构建一个新应用，并希望使用 JavaScript 开发所有的东西
  - 正在使用 React Native 开发少量的二级页面：不需要与应用程序的其他部分有密切联系，但整体观感却更像是“原生”的。
  - 有一个使用 Swift/Java/Objective-C/Kotlin 开发的应用程序，现在你想要使用 React Native 开发其中的一部分。不适合，数据保存方法的不一致
  - 公司里有一个 iOS 团队和一个 Android 团队：要让原生开发和 React Native 开发在企业中大规模并存仍然很困难

## [安装](https://facebook.github.io/react-native/docs/getting-started.html)

```sh
# windows
# Chocolatey（ 基于Nuget的Windows包管理工具）安装与使用
# 以管理员身份运行cmd：
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"

# choco install | uninstall | upgrade package/package
choco install python2
choco install nodejs  # 优化npm镜像
choco install jdk8
```

- 安装 Android Studio
  - Android Studio的欢迎界面中选择Configure | SDK Manager
    - SDK Platforms(Android 6.0 (Marshmallow):Show Package Details)
      - Google APIs
      - Android SDK Platform 23
      - Intel x86 Atom_64 System Image
      - Google APIs Intel x86 Atom_64 System Image
    - SDK Tools(Show Package Details)
      - Android SDK Build-Tools:23.0.1
  - 添加用户变量ANDROID_HOME，sdk地址：D:\Tool\Android\sdk
  - 新建项目运行，保证有物理机或者一个AVD
- 项目构建

```sh
# 安装react-native-cli
npm install -g react-native-cli
# 初始化项目
react-native init AwesomeProject
#  运行应用
cd AwesomeProject
react-native run-android
react-native run-ios

sudo xcode-select -s /Applications/Xcode8.1.app/Contents/Developer/    # （红色部分是你实际的xcode app的名称）

lsof -i tcp:8081
```

### Mac

```shell
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

brew install node yarn
npm config set registry https://registry.npm.taobao.org --global
npm config set disturl https://npm.taobao.org/dist --global

npm install -g yarn react-native-cli
yarn config set registry https://registry.npm.taobao.org --global
yarn config set disturl https://npm.taobao.org/dist --global
sudo chown -R `whoami` /usr/local

brew install watchman # 监视文件系统变更的工具。安装此工具可以提高开发时的性能（packager可以快速捕捉文件的变化从而实现实时刷新）
brew install flow # 静态的JS类型检查工具
xcode

apm install nuclide # 由Facebook提供的基于atom的集成开发环境，可用于编写、运行和 调试React Native应用

react-native init AwesomeProject  # 新建一个项目
cd AwesomeProject
react-native run-android
react-native run-ios
```

## 配置

```
{
  "name": "flickr-client",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
    "react-scripts": "^2.1.8"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "proxy": "http://localhost:4000"
}

```

### JSX

* react.js 、react-dom.js 和 Browser.js ，它们必须首先加载。其中，react.js 是 React 的核心库，react-dom.js 是提供与 DOM 相关的功能，Browser.js 的作用是将 JSX 语法转为 JavaScript 语法
* 写 HTML 标签或 React 标签，它们终将被转换成原生的 JavaScript 并创建 DOM。

```typescript
<script type="text/babel">
  // ** Our code goes here! **
</script>

ReactDOM.render(
  <div>
  {
    names.map(function (name) {
      return <div>Hello, {name}!</div>
    })
  }
  </div>,
  document.getElementById('example')
);

```

### 组件

* React Router是React中使用的路由库，通过管理URL来管理组件及对应的状态。Router组件本身只是一个容器，真正的路由要通过Route组件定义。Router组件支持嵌套路由、支持通配符，能让你轻松控制整个项目的路由结构。
* Redux跟React没有直接的关系，本身可以支持React、Angular、Ember等等框架。Redux其实是Flux-like 更优雅的写法。通过react-redux这个库，可以方便的将react和redux结合起来：React负责页面展现，Redux负责维护/更新数据状态。大致过程为：当用户在View中触发事件产生Action，Action 进到 Reducer，Reducer根据Action Type去匹配对应处理的动作，然后返回一个新的状态。View则因为检测到状态更新而进行重绘。Redux只有一个Store负责存放整个App的状态，而唯一能改变状态的方法只有发送Action。Redux社区中使用比较多的库有：redux-sagas、redux-gen、redux-loop、redux-effects、redux-side-effects、redux-thunks、rx-redux、redux-rx…

```typescript
var HelloMessage = React.createClass({
  render: function() {
    return <h1>Hello {this.props.name}</h1>;
  }
});

ReactDOM.render(
  <HelloMessage name="John" />,
  document.getElementById('example')
);
```

#### Flexbox

Flexbox 是css3 里面引入的布局模型－弹性盒子模型，旨在通过弹性的方式来对齐河分布容器中的内容空间，使其能够适应不同屏幕的宽度。react nativie中 的flexbox 是这个规范的一个子集

* 浮动布局
* 不同宽度屏幕的适
* 宽度自动分配
* 水平垂直居中
* 容器属性
  - flexDirection ： row,row-reverse,colum,colum-reverse   #类型于linerlayout 里的 orientation 属性
  - flexWrap       :   wap,nowap,wap-reverse                      #textview 是否换行
  - alignItems    ： flex-start,flex-end,center,stretch    # item 的 排列对齐方式 ，上对齐，下对齐 上下间距对齐， 以及严苛对其
  - justifyContent：flex-start,flex-end,center,space-between,space-roud  # 类似于linerlayout里 layout_gravity 属性
* 元素属性
  - flex          ：number                     #类型于weight 属性
  - alignSelf     ：atuo,flex-start,flex-end,center,stretch  #类似于 gravity 属性
  - flex－flow  flexDirection 和 flexWrap 属性 的简写形式，默认值为 row nowrap

![lifecycle](../../_static/RN-lifecycle.jpg "lifecycle")

## ReactJS

- 高效：React通过虚拟DOM和Diff算法，最大限度地减少与DOM的交互和渲染。——提高运行效率
- 组件化：通过 React 构建组件，使得代码更加容易复用，适应大型项目开发。——提高可维护性和复用性以及开发效率
- 模块化：通过模块化工具库来解决模块化问题——提高可维护性和复用性
- 单向数据流：React 实现了单向响应的数据流，从而减少了重复代码，这也是它为什么比传统数据绑定更简单。提高可维护性。

生命周期
![](../../_static/react_lifecircle.png)

## [react-native-web](https://necolas.github.io/react-native-web/docs/?path=/docs/*)

## 前后端分离

* Web端通过ajax调用接口，使用JS把数据渲染到页面上
* 数据结构和业务逻辑混淆在一起
* 前后端分离的意义主要在于解耦，解耦后前后端职责划分更明确，前端能做的事也越来越多，比如我们可以在Node层做些监控和日志管理，将SSO登录集成进Node层，使用PM2对Node做多进程管理。这样之后，后端项目就可以做成”微服务”式的架构。
* 后端项目”微服务”式架构有如下优势：
  - 每个项目都很有针对性，仅关注某个业务方向
  - 每个项目可由不同团队独立开发，互不影响，能快速响应需求、及时推出市场
  - 允许在频繁发布不同项目的同时保持系统其他部分的可用性和稳定性：依赖少、构建速度快 & 上线速度快
  - 前端只与Node中间层进行数据通信，Node层则通过thrift接口与后端服务进行数据通信；Node 中间层的 API 设计遵循 RESTFul 的架构风格，并且都以 /api/* 做为前缀；Node 中间层可以视情况添加缓存服务
  - Web端通过ajax调用接口，使用JS把数据渲染到页面上
  - 数据结构和业务逻辑混淆在一起

架构图
![架构图](../_static/front_back_seperate.png)

## 问题

* UI 抽象层翻译出来的 iOS 和安卓原生页面，做不到完全一致，尤其是复杂页面，样式或功能存在差异
* 想用 React Native 做到 iOS 和安卓体验一致，并且充分发挥原生控件的功能，就需要同时熟悉 React Native、iOS、安卓三个平台，这对开发者的要求实在太高了Airbnb 公司在使用 React Native 两年后，宣布放弃，改用原生技术栈

## 图书

* React Native入门与实战
* React Native开发指南
* React Native精解与实战

## 工具

* [Expo](https://expo.io/):The fastest way to build an app
* [uber/baseweb](https://github.com/uber/baseweb):A React Component library implementing the Base design language https://baseweb.design
* [react-hook-form/react-hook-form](https://github.com/react-hook-form/react-hook-form):clipboard React hooks for form validation without the hassle. https://react-hook-form.com
* JSX
  - [developit/htm](https://github.com/developit/htm):Hyperscript Tagged Markup: JSX alternative using standard tagged templates, with compiler support.
* Map
  - [Coder-JJ/rc-leaflet](https://github.com/Coder-JJ/rc-leaflet):React Map Components of Leaflet.js
* IDE
    - [REACTIDE](http://reactide.io)
    - [reactstudio](https://reactstudio.com)
* 状态
    - [jamiebuilds/unstated](https://github.com/jamiebuilds/unstated):State so simple, it goes without saying https://unstated.io
    - [mweststrate/immer](https://github.com/mweststrate/immer):Create the next immutable state by mutating the current one
* 编辑器
    - [facebook/draft-js](https://github.com/facebook/draft-js):A React framework for building text editors. https://draftjs.org/
    - [nikgraf/awesome-draft-js](https://github.com/nikgraf/awesome-draft-js):Awesome list of Draft.js resources
    - [React Studio](https://reactstudio.com/)
    - [margox/braft-editor](https://github.com/margox/braft-editor):美观易用的React富文本编辑器，基于draft-js开发 https://braft.margox.cn/
* 框架
    - [kusti8/proton-native](https://github.com/kusti8/proton-native):A React environment for cross platform native desktop apps https://proton-native.js.org
    - [ReactiveX/rxjs](https://github.com/ReactiveX/rxjs):A reactive programming library for JavaScript http://reactivex.io/rxjs
    - [umijs/umi](https://github.com/umijs/umi):🌋 Pluggable enterprise-level react application framework. https://umijs.org/
    - [Microsoft/reactxp](https://github.com/microsoft/reactxp):Library for cross-platform app development. https://microsoft.github.io/reactxp/
    - [alibaba/ice](https://github.com/alibaba/ice/):🚀 飞冰 - 让前端开发简单而友好，海量可复用物料，配套桌面工具极速构建前端应用，效率提升 100% https://alibaba.github.io/ice/
* 开发工具
    - [facebook/react-devtools](https://github.com/facebook/react-devtools):An extension that allows inspection of React component hierarchy in the Chrome and Firefox Developer Tools.
    - [gaearon/redux-devtools](https://github.com/gaearon/redux-devtools):DevTools for Redux with hot reloading, action replay, and customizable UI http://youtube.com/watch?v=xsSnOQynTHs
    - [transitive-bullshit/create-react-library](https://github.com/transitive-bullshit/create-react-library):⚡CLI for easily creating reusable react libraries.
* Angular
    - [ngrx/platform](https://github.com/ngrx/platform):Reactive libraries for Angular
* 设计模式
    - [chantastic/reactpatterns.com](https://github.com/chantastic/reactpatterns.com):Patterns for React Developers http://reactpatterns.com
* 图表
    - [hshoff/vx](https://github.com/hshoff/vx):🐯react + d3 = vx | visualization components https://vx-demo.now.sh/
    - [react-native-community/react-native-linear-gradient](https://github.com/react-native-community/react-native-linear-gradient):A <LinearGradient /> component for react-native
    - [nadbm/react-datasheet](https://github.com/nadbm/react-datasheet):Excel-like data grid component for react https://nadbm.github.io/react-datasheet/
    - [hustcc/echarts-for-react](https://github.com/hustcc/echarts-for-react):📈 baidu Echarts(v3.0 & v4.0) components for React wrapper. 一个简单的 echarts(v3.0 & v4.0) 的 react 封装 https://git.hust.cc/echarts-for-react
* 表单
    - [mozilla-services/react-jsonschema-form](https://github.com/mozilla-services/react-jsonschema-form):A React component for building Web forms from JSON Schema.
    - [jaredpalmer/formik](https://github.com/jaredpalmer/formik):Build forms in React, without the tears 😭 https://jaredpalmer.com/formik
* 图片
    - [ricardo-ch/react-easy-crop](https://github.com/ricardo-ch/react-easy-crop):A React component to crop images with easy interactions https://codesandbox.io/s/q80jom5ql6
    - [xiaolin/react-image-gallery](https://github.com/xiaolin/react-image-gallery):React carousel image gallery component with thumbnail and mobile support
    - [smooth-code/svgr](https://github.com/smooth-code/svgr):Transform SVGs into React components 🦁 https://svgr.now.sh/
* 文件
    - [diegomura/react-pdf](https://github.com/diegomura/react-pdf):📄 Create PDF files using React http://react-pdf.diegomura.com/repl
* animations
    - [react-tools/react-move](https://github.com/react-tools/react-move):React Move 🌀 Beautiful, data-driven animations for React https://react-move.js.org
    - [react-dnd/react-dnd](https://github.com/react-dnd/react-dnd):Drag and Drop for React http://react-dnd.github.io/react-dnd
    - [react-beautiful-dnd](https://github.com/atlassian/react-beautiful-dnd):Beautiful and accessible drag and drop for lists with React https://react-beautiful-dnd.netlify.com/
    - [react-spring/react-spring](https://github.com/react-spring/react-spring):✌️ A spring physics based React animation library https://react-spring.github.iov
* 脚手架
  - [youzan/zent-kit](https://github.com/youzan/zent-kit)React 组件库开发脚手架
  - [rekit](https://github.com/rekit/rekit):IDE and toolkit for building scalable web applications with React, Redux and React-router [http://rekit.js.org](http://rekit.js.org/)
* firebase
    - [invertase/react-native-firebase](https://github.com/invertase/react-native-firebase):🔥 A well tested feature rich modular Firebase implementation for React Native. Supports both iOS & Android platforms for over 15 Firebase services.https://rnfirebase.io/
    - [kriasoft/react-firebase-starter](https://github.com/kriasoft/react-firebase-starter)：Boilerplate (seed) project for creating web apps with React.js, GraphQL.js and Relay https://firebase.reactstarter.com
* 渲染
    - [stereobooster/react-snap](https://github.com/stereobooster/react-snap):👻 Zero-configuration framework-agnostic static prerendering for SPAs
    - [renatorib/react-powerplug](https://github.com/renatorib/react-powerplug):🔌 Renderless Containers
* 命令行
    - [maicki/why-did-you-update](https://github.com/maicki/why-did-you-update):💥 Puts your console on blast when React is making unnecessary updates.
    - [vadimdemedes/ink](https://github.com/vadimdemedes/ink):🌈 React for interactive command-line apps
* 按钮
    - [transitive-bullshit/react-particle-effect-button](https://github.com/transitive-bullshit/react-particle-effect-button):Bursting particle effect buttons for React 🎉
    - [greena13/react-hotkeys](https://github.com/greena13/react-hotkeys):Declarative hotkey and focus area management for React
* WEB
    - [taobaofed/react-web](https://github.com/taobaofed/react-web):A framework for building web apps with React Native compatible API. http://taobaofed.github.io/react-web/
* i18n
    - [lingui/js-lingui](https://github.com/lingui/js-lingui):🌍📖 A readable, automated, and optimized (5 kb) internationalization for JavaScript and React https://lingui.js.org/
    - [i18next/react-i18next](https://github.com/i18next/react-i18next):Internationalization for react done right. Using the i18next i18n ecosystem. https://react.i18next.com/
* SPA
    - [stereobooster/react-snap](https://github.com/stereobooster/react-snap):👻 Zero-configuration framework-agnostic static prerendering for SPAs
* 代码展示
    - [pomber/code-surfer](https://github.com/pomber/code-surfer):React component for scrolling, zooming and highlighting code <🏄/>
* Docker
    - [zzswang/docker-nginx-react](https://github.com/zzswang/docker-nginx-react):Run react single page app within a nginx server
* Cookies
    - [reactivestack/cookies](https://github.com/reactivestack/cookies):Load and save cookies within your React application
* 地图
    - [mariusandra/pigeon-maps](https://github.com/mariusandra/pigeon-maps):ReactJS Maps without external dependencies
* 代码检测
    - [facebook/prop-types](https://github.com/facebook/prop-types):Runtime type checking for React props and similar objects
* 搜索
    - [searchkit/searchkit](https://github.com/searchkit/searchkit):React UI components / widgets. The easiest way to build a great search experience with Elasticsearch. http://www.searchkit.co
* 文档
    - [nfl/react-helmet](https://github.com/nfl/react-helmet):A document head manager for React
    - [reactjs/react-docgen](https://github.com/reactjs/react-docgen):A CLI and toolbox to extract information from React component files for documentation generation purposes.
* 测试
    - [kentcdodds/react-testing-library](https://github.com/kentcdodds/react-testing-library):🐐 Simple and complete React DOM testing utilities that encourage good testing practices. http://npm.im/react-testing-library
    - [airbnb/enzyme](https://github.com/airbnb/enzyme):JavaScript Testing utilities for React https://airbnb.io/enzyme/
* 编辑器
    - [jpuri/react-draft-wysiwyg](https://github.com/jpuri/react-draft-wysiwyg):A Wysiwyg editor build on top of ReactJS and DraftJS. https://jpuri.github.io/react-draft-wysiwyg
    - [rexxars/react-markdown](https://github.com/rexxars/react-markdown):Render Markdown as React components
* Bundler
    - [facebook/metro](https://github.com/facebook/metro):🚇 The JavaScript bundler for React Native. https://facebook.github.io/metro
* 地图
    - [yezihaohao/react-qmap](https://github.com/yezihaohao/react-qmap):💡react腾讯地图开源组件 https://cheng_haohao.gitee.io/reactqmap
* 测试
    - [kentcdodds/react-testing-library](https://github.com/kentcdodds/react-testing-library):🐐 Simple and complete React DOM testing utilities that encourage good testing practices. http://npm.im/react-testing-library
* 路由
    - [reactjs/redux](https://github.com/reactjs/redux):Predictable state container for JavaScript apps http://redux.js.org
    - [ReactTraining/react-router](https://github.com/ReactTraining/react-router):Declarative routing for React https://reacttraining.com/react-router/
    - [aksonov/react-native-router-flux](https://github.com/aksonov/react-native-router-flux):First Declarative React Native Router
    - [camsong/redux-in-chinese](https://github.com/camsong/redux-in-chinese):Redux 中文文档 http://cn.redux.js.org/
    - [reach/router](https://github.com/reach/router):Next Generation Routing for React https://reach.tech/router
    - [markerikson/react-redux-links](https://github.com/markerikson/react-redux-links):Curated tutorial and resource links I've collected on React, Redux, ES6, and more
    - [redux-offline/redux-offline](https://github.com/redux-offline/redux-offline):Build Offline-First Apps for Web and React Native
    - [acdlite/redux-router](https://github.com/acdlite/redux-router):Redux bindings for React Router – keep your router state inside your Redux store
    - [erikras/react-redux-universal-hot-example](https://github.com/erikras/react-redux-universal-hot-example):A starter boilerplate for a universal webapp using express, react, redux, webpack, and react-transform
    - [maicki/react-native-router-bridge](https://github.com/maicki/react-native-router-bridge):Small module which bridges the navigation world between native and React Native.
* gesture
    - [kmagiera/react-native-gesture-handler](https://github.com/kmagiera/react-native-gesture-handler):Declarative API exposing platform native touch and gesture system to React Native.
* Hooks
    - [rehooks/awesome-react-hooks](https://github.com/rehooks/awesome-react-hooks):Awesome React Hooks
    - [zeit/swr](https://github.com/zeit/swr):React Hooks library for remote data fetching https://swr.now.sh
* 组件
    - [brillout/awesome-react-components](https://github.com/brillout/awesome-react-components):Catalog of React Components & Libraries https://devarchy.com/react
    - [AllenFang/react-bootstrap-table](https://github.com/AllenFang/react-bootstrap-table):A Bootstrap table built with React.js https://allenfang.github.io/react-boo…
    - [React-Bootstrap](https://github.com/react-bootstrap/react-bootstrap)
    - [akiran/react-slick](https://github.com/akiran/react-slick):React carousel component http://neostack.com/opensource/react-…
    - [react-boilerplate/react-boilerplate](https://github.com/react-boilerplate/react-boilerplate):A highly scalable, offline-first foundation with the best developer experience and a focus on performance and best practices. https://www.reactboilerplate.com
    - [airbnb/react-dates](https://github.com/airbnb/react-dates):An easily internationalizable, mobile-friendly datepicker library for the web http://airbnb.io/react-dates
    - [airbnb/lottie-android](https://github.com/airbnb/lottie-android):Render After Effects animations natively on Android and iOS, Web, and React Native http://airbnb.io/lottie/
    - [airbnb/lottie-ios](https://github.com/airbnb/lottie-ios):An iOS library to natively render After Effects vector animations http://airbnb.io/lottie/
    - [airbnb/react-native-maps](https://github.com/airbnb/react-native-maps):React Native Mapview component for iOS + Android
    - [airbnb/native-navigation](https://github.com/airbnb/native-navigation):Native navigation library for React Native applications http://airbnb.io/native-navigation/
    - [react-navigation/react-navigation](https://github.com/react-navigation/react-navigation):Routing and navigation for your React Native apps https://reactnavigation.org
    - [apollographql/react-apollo](https://github.com/apollographql/react-apollo):♻️ React integration for Apollo Client https://www.apollographql.com/docs/react/

    - [maisano/react-router-transition](https://github.com/maisano/react-router-transition):painless transitions built for react-router, powered by react-motion
    - [jaredpalmer/formik](https://github.com/jaredpalmer/formik):Build forms in React, without the tears sob https://npm.im/formik
    - [Hacker0x01/react-datepicker](https://github.com/Hacker0x01/react-datepicker):A simple and reusable datepicker component for React https://reactdatepicker.com/
    - [ptmt/react-native-macos](https://github.com/ptmt/react-native-macos):React Native for macOS is an experimental fork for writing desktop apps using Cocoa
    - [oblador/react-native-vector-icons](https://github.com/oblador/react-native-vector-icons):Customizable Icons for React Native with support for NavBar/TabBar/ToolbarAndroid, image source and full styling.
    - [rt2zz/redux-persist](https://github.com/rt2zz/redux-persist):persist and rehydrate a redux store
    - [necolas/react-native-web](https://github.com/necolas/react-native-web):React Native for Web
    - [react-native-training/react-native-elements](https://github.com/react-native-training/react-native-elements):Cross Platform React Native UI Toolkit
    - [invertase/react-native-firebase](https://github.com/invertase/react-native-firebase):A well tested feature rich modular Firebase implementation for React Native, supporting both iOS & Android platforms for 15+ Firebase modules (including a feature rich Notifications implementation) 🔥 https://rnfirebase.io
    - [coryhouse/react-slingshot](https://github.com/coryhouse/react-slingshot):React + Redux starter kit / boilerplate with Babel, hot reloading, testing, linting and a working example app built in
    - [reactjs/react-docgen](https://github.com/reactjs/react-docgen):A CLI and toolbox to extract information from React component files for documentation generation purposes.
    - [oney/react-native-webrtc](https://github.com/oney/react-native-webrtc):A WebRTC module for React Native.
    - [react-dnd/react-dnd](https://github.com/react-dnd/react-dnd):Drag and Drop for React http://react-dnd.github.io/react-dnd
    - [atlassian/react-beautiful-dnd](https://github.com/atlassian/react-beautiful-dnd):Beautiful, accessible drag and drop for lists with React.js
    - [drcmda/react-spring](https://github.com/drcmda/react-spring):🙌 Helping react-motion and animated to become best friends http://react-spring.surge.sh/
    - [deepsweet/hocs](https://github.com/deepsweet/hocs):🍱 A collection of Higher-Order Components for React and React Native
    - [React toolbox](https://github.com/react-toolbox/react-toolbox)
    - [React Belle](https://github.com/nikgraf/belle)
    - [React Grommet](http://grommet.io/)
    - [Halogen](http://ww12.madscript.com/):制作酷酷的载入进度条
    - [rjsf-team/react-jsonschema-form](https://github.com/rjsf-team/react-jsonschema-form):A React component for building Web forms from JSON Schema.
    - [React UWP](https://github.com/myxvisual/react-uwp):Windows 下的 UI 框架实现了微软的 UWP 和 Fluent，提供了全面的控件库以实现 UI 可视化呈现，以及用于其它控件或内容（如图像和媒体）的容器。
    - [UXCore](link):40 个为企业应用设计的组件，专注于后端应用的性能，主要是表格和表单这些组件（特别是当数据自动与视图绑定时）。
    - [reasonml/reason-react](https://github.com/reasonml/reason-react):Reason bindings for ReactJS https://reasonml.github.io/reason-react/
    - [reactjs/react-transition-group](https://github.com/reactjs/react-transition-group):An easy way to perform animations when a React component enters or leaves the DOM
    - [clauderic/react-sortable-hoc](https://github.com/clauderic/react-sortable-hoc):A set of higher-order components to turn any list into an animated, touch-friendly, sortable list ✌️
    - [streamich/libreact](https://github.com/streamich/libreact):Collection of useful React components
    - [jaredpalmer/formik](https://github.com/jaredpalmer/formik):Build forms in React, without the tears 😭 https://jaredpalmer.com/formik
    - [JedWatson/react-select](https://github.com/JedWatson/react-select):The Select for React.js https://react-select.com/
    - [styled-components/styled-components](https://github.com/styled-components/styled-components):Visual primitives for the component age. Use the best bits of ES6 and CSS to style your apps without stress 💅 https://styled-components.com
    - [paypal/downshift](https://github.com/paypal/downshift):🏎 Primitive to build simple, flexible, WAI-ARIA compliant enhanced input React components http://downshift.netlify.com/
    - [tajo/react-portal](https://github.com/tajo/react-portal):React component for transportation of modals, lightboxes, loading bars... to document.body or else.
    - [jasonslyvia/react-lazyload](https://github.com/jasonslyvia/react-lazyload):Lazy load your component, image or anything matters the performance.
    - [react-component/upload](https://github.com/react-component/upload):React Upload http://react-component.github.io/upload/
    - [zenoamaro/react-quill](https://github.com/zenoamaro/react-quill):A Quill component for React. https://zenoamaro.github.io/react-quill
    - [aholachek/react-flip-toolkit](https://github.com/aholachek/react-flip-toolkit):An animation utility library for highly configurable layout transitions
    - [sokra/rawact](https://github.com/sokra/rawact):[POC] A babel plugin which compiles React.js components into native DOM instructions to eliminate the need for the react library at runtime.
    - [Bogdan-Lyashenko/Under-the-hood-ReactJS](https://github.com/Bogdan-Lyashenko/Under-the-hood-ReactJS):Entire React code base explanation by visual block schemes (Stack version)
    - [FormidableLabs/react-live](https://github.com/FormidableLabs/react-live):A production-focused playground for live editing React components https://react-live.kitten.sh/
    - [RubyLouvre/anu](https://github.com/RubyLouvre/anu):the React16-compat mini library https://rubylouvre.github.io/nanachi/ https://rubylouvre.github.io/anu/
    - [wix/react-native-interactable](https://github.com/wix/react-native-interactable):Experimental implementation of high performance interactable views in React Native
    - [alibaba-fusion/next](https://github.com/alibaba-fusion/next):A configurable component library for web built on React. https://fusion.design
    - [react-native-debugger](https://github.com/jhen0409/react-native-debugger)
* [redux-saga/redux-saga](https://github.com/redux-saga/redux-saga):An alternative side effect model for Redux apps https://redux-saga.js.org/
* [acdlite/recompose](https://github.com/acdlite/recompose):A React utility belt for function components and higher-order components.
* [jamiebuilds/react-loadable](https://github.com/jamiebuilds/react-loadable):⏳ A higher order component for loading components with promises.
* template
  - [erikras / react-redux-universal-hot-example](https://github.com/erikras/react-redux-universal-hot-example)  A starter boilerplate for a universal webapp using express, react, redux, webpack, and react-transform

## UI

* [gestalt](https://github.com/pinterest/gestalt):一组支持 Pinterest 设计语言的 React UI 组件，被 Pinterest 内部用来实现统一的 UI 设计和开发
* [IBM/carbon-components](https://github.com/IBM/carbon-components):The component library behind the Carbon Design System https://www.carbondesignsystem.com
* [React Foundation](https://github.com/digiaonline/react-foundation):将 Foundation 的所有部分都包装成可复用的 React 组件，它专注于易用性和灵活性，尽可能使用无状态的组件
* [OfficeDev/office-ui-fabric-react](https://github.com/OfficeDev/office-ui-fabric-react):React components for building experiences for Office and Office 365. https://developer.microsoft.com/en-us/fabric#/components
* [Atlaskit](https://atlaskit.atlassian.com/):Atlassian 的官方 React UI 套件是 [Atlassian 设计指南](https://atlassian.design/)的实现。它提供了一组可复用的组件，均可独立下载到开发者的项目中
* [jxnblk/rebass](https://github.com/jxnblk/rebass):⚛️ React UI component library & design system, built with styled-components and styled-system. http://jxnblk.com/rebass
* [elementalui/elemental](https://github.com/elementalui/elemental):A flexible and beautiful UI framework for React.js http://elemental-ui.com
* [primefaces/primereact](https://github.com/primefaces/primereact):UI Components for React
* [reactstrap/reactstrap](https://github.com/reactstrap/reactstrap):Simple React Bootstrap 4 components https://reactstrap.github.io
* [React MD](https://github.com/mlaursen/react-md):提供了用于开发 Web 应用的套件，遵循谷歌 Material Design 设计原则，还有高度定制化的主题和样式
* [Blueprint](https://github.com/palantir/blueprint):提供了一系列 React UI 组件，这些组件包含常用的元素、模式和 Web 交互
* [React Virtualized](https://github.com/bvaughn/react-virtualized):可以高效渲染大型列表和表格数据的 React 组件
* [Semantic UI React](https://react.semantic-ui.com/introduction):官方的 Semantic-UI-React 集成，提供了有趣、灵活的工具，已被 Netflix 和 Amazon 采用。
* [Material Components Web](https://github.com/material-components/material-components-web/):组件使用可靠的开发工作流程来构建漂亮而实用的 Web 项目
* [jxnblk/grid-styled](https://github.com/jxnblk/grid-styled):Responsive React grid system built with styled-system https://jxnblk.com/grid-styled/
* [segmentio/evergreen](https://github.com/segmentio/evergreen):🌲 Evergreen React UI Framework by Segment https://evergreen.surge.sh/
* [gabrielbull/react-desktop](https://github.com/gabrielbull/react-desktop):React UI Components for macOS Sierra and Windows 10 http://reactdesktop.js.org
* [mui-org/material-ui](https://github.com/mui-org/material-ui):React components that implement Google's Material Design. https://material-ui.com
* [GeekyAnts/NativeBase](https://github.com/GeekyAnts/NativeBase):Essential cross-platform UI components for React Native https://nativebase.io/
* [uiw-react/uiw](https://github.com/uiw-react/uiw):@uiw-react A high quality UI Toolkit, A Component Library for React 16+. https://uiw-react.github.io
* [reakit/reakit](https://github.com/reakit/reakit):Toolkit for building interactive UIs with React https://reakit.io
* [pinterest/gestalt](https://github.com/pinterest/gestalt):A set of React UI components that supports Pinterest’s design language https://pinterest.github.io/gestalt
* [segmentio/evergreen](https://github.com/segmentio/evergreen):🌲 Evergreen React UI Framework by Segment https://evergreen.surge.sh/
* [JetBrains/ring-ui](https://github.com/JetBrains/ring-ui):A collection of JetBrains Web UI components https://jetbrains.github.io/ring-ui
* [xotahal/react-native-material-ui](https://github.com/xotahal/react-native-material-ui):Highly customizable material design components for React Native
* [miukimiu/react-kawaii](https://github.com/miukimiu/react-kawaii):Cute React UI Components https://react-kawaii.now.sh/
* [mui-org/material-ui](https://github.com/mui-org/material-ui):React components that implement Google's Material Design. https://material-ui.com/
* [xinthink/react-native-material-kit](https://github.com/xinthink/react-native-material-kit):Bringing Material Design to React Native http://j.mp/rnmdk
* [Semantic-Org/Semantic-UI-React](https://github.com/Semantic-Org/Semantic-UI-React):The official Semantic-UI-React integration https://react.semantic-ui.com
* [shoutem/ui](https://github.com/shoutem/ui):Customizable set of components for React Native applications

## 项目

* [trazyn/ieaseMusic](https://github.com/trazyn/ieaseMusic):这应该是最好的网易云音乐播放器了，没有之一，如果有请打醒 🤘
* [Binaryify/NeteaseCloudMusicApi](https://github.com/Binaryify/NeteaseCloudMusicApi):网易云音乐nodejs api https://binaryify.github.io/NeteaseCl…
* [JonJam/yorpw_ui_web](https://github.com/JonJam/yorpw_ui_web):Password manager SPA built using React and Redux
* [JonJam/react-redux-ts](https://github.com/JonJam/react-redux-ts):React/Redux TypeScript starter project
* [taikongfeizhu/webpack-develop-startkit](https://github.com/taikongfeizhu/webpack-develop-startkit):webpack-develop-startkit
* [duxianwei520/react](https://github.com/duxianwei520/react):一个react+redux+webpack+ES6+antd的SPA的后台管理底层框架
* [fbsamples/f8app](https://github.com/fbsamples/f8app):Source code of the official F8 app of 2017, powered by React Native and other Facebook open source projects. http://makeitopen.com
* [EleTeam/Shop-React-Native](https://github.com/EleTeam/Shop-React-Native):EleTeam开源项目 - 电商全套解决方案之 React Native 版 - Shop-React-Native。一个类似京东/天猫/淘宝的商城，有对应的服务端支持，由EleTeam团队维护！
* [tyroprogrammer/learn-react-app](https://github.com/tyroprogrammer/learn-react-app):Application that will help you learn React fundamentals. Install this application locally - there's tutorial, code snippets and exercises. The main objective of this project is to help you get off the ground with React!
* [microsoft/TypeScript-React-Starter](https://github.com/Microsoft/TypeScript-React-Starter):A starter template for TypeScript and React with a detailed README describing how to use the two together.
* [CarGuo/GSYGithubAPP](https://github.com/CarGuo/GSYGithubApp)

## 参考

* [React Native的极简手册](http://www.jianshu.com/p/318342e139c7)
* [reactnativecn/react-native-guide](https://github.com/reactnativecn/react-native-guide):React Native指南汇集了各类react-native学习资源、开源App和组件
* [styleguidist/react-styleguidist](https://github.com/styleguidist/react-styleguidist):Isolated React component development environment with a living style guide https://react-styleguidist.js.org/
* [wojtekmaj/react-lifecycle-methods-diagram](https://github.com/wojtekmaj/react-lifecycle-methods-diagram):Interactive React lifecycle methods diagram. http://projects.wojtekmaj.pl/react-li…
* [react-native-elements](https://github.com/react-native-training/react-native-elements):Cross Platform React Native UI Toolkit https://react-native-training.github.…
* [jondot/awesome-react-native](https://github.com/jondot/awesome-react-native):Awesome React Native components, news, tools, and learning material! http://www.awesome-react-native.com
* [enaqx/awesome-react](https://github.com/enaqx/awesome-react)A collection of awesome things regarding React ecosystem.

* [fangwei716/30-days-of-react-native](https://github.com/fangwei716/30-days-of-react-native)30 days of React Native demos
* [reactjs/react-basic](https://github.com/reactjs/react-basic):A description of the conceptual model of React without implementation burden.
* [React 生态系统：从小白到大神](http://blog.csdn.net/gitchat/article/details/77978708)

* [streamich/react-use](https://github.com/streamich/react-use):React Hooks — future of React 👍 react-use http://streamich.github.io/react-use
* [davezuko/react-redux-starter-kit](https://github.com/davezuko/react-redux-starter-kit):Get started with React, Redux, and React-Router.
* [kriasoft/react-starter-kit](https://github.com/kriasoft/react-starter-kit):React Starter Kit — isomorphic web app boilerplate (Node.js, Express, GraphQL, React.js, Babel, PostCSS, Webpack, Browsersync) https://reactstarter.com
* [adam-golab/react-developer-roadmap](https://github.com/adam-golab/react-developer-roadmap):Roadmap to becoming a React developer in 2018s
* [kentcdodds/advanced-react-patterns](https://github.com/kentcdodds/advanced-react-patterns):The course material for my advanced react patterns course on Egghead.io
* [huzidaha/react-naive-book](https://github.com/huzidaha/react-naive-book):开源、免费、专业、简单的 React.js 在线教程 http://huziketang.com/books/react
* [ruanyf/react-demos](https://github.com/ruanyf/react-demos):a collection of simple demos of React.js
* [30-seconds/30-seconds-of-react](https://github.com/30-seconds/30-seconds-of-react):Curated collection of useful React snippets that you can understand in 30 seconds or less.
* [React 开发必须知道的 34 个技巧](https://juejin.im/post/5dcb5a80e51d4520db19b906)

* [设计含结构](https://github.com/airbnb/react-sketchapp)
* [文档](http://airbnb.io/react-sketchapp/docs/)
* [文档](http://reactnative.cn/docs/0.49/getting-started.html)
* [sw-yx/react-typescript-cheatsheet](https://github.com/sw-yx/react-typescript-cheatsheet)

* [vasanthk/react-bits](https://github.com/vasanthk/react-bits):✨ React patterns, techniques, tips and tricks ✨ https://vasanthk.gitbooks.io/react-bits
* [react-pxq](https://github.com/bailicangdu/react-pxq)一个 react + redux 的完整项目 和 个人总结

* [youzan/zent](https://github.com/youzan/zent)A collection of essential UI components written with React.
* [vhpoet/react-native-styling-cheat-sheet](https://github.com/vhpoet/react-native-styling-cheat-sheet):Most of the React Native styling material in one page
* [tachyons-css/tachyons](https://github.com/tachyons-css/tachyons/):Functional css for humans https://tachyons.io
* [React Native精解与实践](link)
* 《React 学习之道》
* [Learn the Basics](https://facebook.github.io/react-native/docs/tutorial)
