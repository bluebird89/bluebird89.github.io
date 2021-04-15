# [angular.js](https://github.com/angular/angular.js)

AngularJS - HTML enhanced for web apps! <https://angularjs.org>

* AngularJS 是 Google 于 2009 年发布的 Web 增强框架，一度作为 Web 开发主流方案，但是随着 Google 宣布 AngularJS 的 final LTS 计划
* 渐进式Web应用：借助现代化Web平台的力量，交付app式体验。高性能、离线化、零安装。
* 原生：借助来自Ionic、NativeScript和React Native中的技术与思想，构建原生移动应用。
* 桌面：借助你已经在Web开发中学过的能力，结合访问原生操作系统API的能力，创造能在桌面环境下安装的应用，横跨Mac、Windows和Linux平台。
* 代码生成:Angular会把你的模板转换成代码，针对现代JavaScript虚拟机进行高度优化，轻松获得框架提供的高生产率，同时又能保留所有手写代码的优点。
* 统一:在服务端渲染应用的首屏，像只有HTML和CSS的页面那样几乎瞬间展现，支持node.js、.NET、PHP，以及其它服务器，为通过SEO来优化站点铺平了道路。
* 代码拆分:Angular应用通过新的组件路由（Component Router）模块实现快速加载，提供了自动拆分代码的功能，为用户单独加载它们请求的视图中需要的那部分代码。
* 模板:通过简单而强大的模板语法，快速创建UI视图。
* Angular命令行工具:命令行工具：快速进入构建环节、添加组件和测试，然后立即部署。
* 各种IDE:在常用IDE和编辑器中获得智能代码补全、实时错误反馈及其它反馈等特性。
* 测试:使用Karma进行单元测试，让你在每次存盘时都能立即知道是否弄坏了什么。Protractor则让你的场景测试运行得又快又稳定。
* 动画:通过Angular中直观简便的API创建高性能复杂编排和动画时间线 —— 只要非常少的代码。
* 可访问性:通过支持ARIA的组件、开发者指南和内置的一体化测试基础设施，创建具有完备可访问性的应用。

## [angular](https://github.com/angular/angular)

One framework. Mobile & desktop. <https://angular.io>

## 项目

```sh
git clone https://github.com/angular/quickstart.git quickstart
cd quickstart
npm install   # 执行npm安装和配置
npm start     # 启动项目

npm run tsc # 单独编译Typescrip到Javascript。
npm run tsc:w # 单独编译Typescrip，并监控文件状态，发现文件变化重新编译
npm run lite  # 启动Server，在浏览器中查看效果。
npm test # 单元测试
npm run e2e  # E2E测试End-to-end
```

### 结构

* app/app.components.ts, 一个自定义组件，Typescript代码。
* app/app.module.ts, 模块文件，用于组合管理组件，Typescript代码。
* app/main.ts, 项目启动的入口，加载ts文件，Typescript代码。
* app/app.components.spec.ts, 单测试文件
* .gitignore, git的配置文件
    * * index.html, 单页应用的html入口文件
* package.json, Node项目的工程配置文件
* tsconfig.json, Typescript语言的配置文件

## [angular/angular-cli](https://github.com/angular/angular-cli)

CLI tool for Angular

```sh
npm install -g @angular/cli

ng help
ng version

ng add <package>
ng add @angular/pwa
ng update <package> # 使用正确版本的依赖包

ng new conan
cd conan
ng serve
ng serve --host 0.0.0.0 --port 4201 --live-reload-port 49153
```

### 模块生成器

* component:组件，生成单独文件以及注册
* directive:属性型指令用于改变一个 DOM 元素的外观或行为。
* service:服务，可以封装代码，比如我们可以对数据访问代码单独隔离，封装到一个独立的服务中
* pipe:管道，可以用于数据的连续处理操作，比如可以把日期在界面端进行格式化

```sh
ng generate component my-new-component # 组件Component

ng generate directive my-new-directive # 指令Directive

ng generate pipe my-new-service # 服务Service
ng generate pipe my-new-pipe # 管道Pipe

ng generate class my-new-class # 类Class

ng generate interface my-new-interface # 接口Interface

ng generate enum my-new-enum # 枚举对象Enum

ng generate service my-service-name

ng generate module my-module # 模块Modulew
```

## hooks

* constructor: The constructor is always called first.
* ngOnInit: This lifecycle hook is called after the constructor.
* ngOnchanges: When the value of an input is changed, this lifecycle hook is executed.
* ngDoCheck: When the input properties are checked, this method will be called.
* ngAfterContentInit: When the content of the component is initialized, this hook is called. A component-only hook.
* ngAfterContentChecked: Called after the content is checked. A component-only hook.
* ngAfterViewInit: After a view is initialized, this hook is called. A component-only hook.
* ngAfterViewChecked: After a view is checked, this hook is called. A component-only hook.
* ngOnDestroy: This method is called before Angular destroys the component/directive.

## 问题

```
# An unhandled exception occurred: NGCC failed.
tsconfig.app.json:
"angularCompilerOptions": {
    "enableIvy": false
},
```

## 图书

* Angular 权威教程

## 教程

* [angularjs-book](https://github.com/shyamseshadri/angularjs-book):Examples and Code snippets from the AngularJS O'Reilly book
* [quickstart](https://github.com/angular/quickstart):Angular 2 QuickStart - source from the documentation
* [官方教程](https://angular.io)：<https://angular.cn/guide/quickstart>
* [angular-starter](https://github.com/gdi2290/angular-starter):🎉 An Angular Starter kit featuring Angular (Router, Http, Forms, Services, Tests, E2E, Dev/Prod, HMR, Async/Lazy Routes, AoT via ngc), Karma, Protractor, Jasmine, Istanbul, TypeScript, TsLint, Codelyzer, Hot Module Replacement, @types, and Webpack by @TipeIO <https://tipe.io> https://angular.realworld.io/

## 项目

* [angular-realworld-example-app](https://github.com/gothinkster/angular-realworld-example-app)Exemplary real world application built with Angular

## 工具

* [ngx-virtual-scroller](https://github.com/rintoj/ngx-virtual-scroller):Virtual Scroll displays a virtual, "infinite" list.
* [angular-cli](https://github.com/angular/angular-cli):CLI tool for Angular <https://cli.angular.io/>
* [nebular](https://github.com/akveo/nebular):Angular 7 Components, Auth and Security <https://akveo.github.io/nebular>
* [angular-loading-bar](https://github.com/chieffancypants/angular-loading-bar):A fully automatic loading / progress bar for your angular apps.
* [platform](https://github.com/ngrx/platform):Reactive libraries for Angular <https://ngrx.io>
* [angular-google-maps](https://github.com/SebastianM/angular-google-maps):Angular 2+ Google Maps Components <https://angular-maps.com/>
* [angularjs-styleguide](https://github.com/toddmotto/angularjs-styleguide):AngularJS styleguide for teams <https://ultimateangular.com>
* UI
  - [material](https://github.com/angular/material):Material design for AngularJS <https://material.angularjs.org/>
  - [material2](https://github.com/angular/material2):Material Design components for Angular <https://material.angular.io>
  - [flex-layout](https://github.com/angular/flex-layout):Provides HTML UI layout for Angular applications; using Flexbox and a Responsive API
* [augury](https://github.com/rangle/augury):Angular Debugging and Visualization Tools <https://augury.angular.io/>
* 升级
  - [ngMigration Assistant](https://github.com/ellamaolson/ngMigration-Assistant):一个命令行工具，用于分析 AngularJS 应用程序，并在此基础上，提出迁移路径建议。同时，它还提供应用程序中代码复杂性、大小、构造等方面的统计信息，告诉你迁移之前必要的准备工作。
  - [ngMigration Forum](https://github.com/angular/ngMigration-Forum/wiki): 是一个社区，聚集了网络上最佳的迁移经验和信息。

* [ngx-admin](https://github.com/akveo/ngx-admin):Admin dashboard template based on Angular 5+, Bootstrap 4 (previously known as ng2-admin) <http://akveo.com/ngx-admin/>

## 参考

* [awesome-angular](https://github.com/gdi2290/awesome-angular):📄 A curated list of awesome Angular resources by @tipeio <https://tipe.io>
* [Top 12 Productivity Tips for WebStorm and Angular – Part 1](https://www.sitepoint.com/productivity-tips-for-webstorm-and-angular-part-1/)
* [Angular2新的体验](http://blog.fens.me/angular2-init/)
