# UI User Interface

原型设计工具：原型设计工具能仿真交互上的一些操作，最终还能将结果导出成 HTML

* 元素
* 交互
* 习惯

## 颜色

* 蓝色用于科技
* 红色用于生活
* 绿色用于生态

## 从Web借鉴UI设计

* 指导原则概述
    - 系统是自描述的:对于好的UI设计系统应该易于使用。无需阅读额外的文档，系统UI本身就能引导用户选择正确的道路。
    - 尽力隐藏系统复杂度 简约风格的UI更易于用户使用。
    - 提示处理过的信息:不要反馈那些用户无法理解的专业术语，这样做不仅会使用户反感，而且会暴露某些敏感信息，要反馈用户自己的语言。
    - 标识引导设计 系统必须清晰地告知用户：他们身在何处？他们寻找的东西在哪里？他们如何到达？
    - 尽快提供反馈 UI应该能够在动作真正发生之前让用户知道动作尚未发生，提醒用户正处在过程中的哪个阶段。
    - 人性化设计 合适的字体大小，温和的背景色，合理的按钮位置。
    - 保持一致，考虑标准 一致的界面风格易于使用，遵循标准更是使应用程序给用户以专业的感觉。
    - 提供验证与纠错 “预防”、“保护”与“通知”是帮助用户改正错误的好的实践。
    - 减轻用户负担 把用户记不住的移交给应用软件处理。
    - 考虑到不同类型与不同水平的用户 从用户使用角度出发，给用户真正想要的，而不是仅靠我们的主观臆测。
    - 提供上下文帮助和文档 虽然自描述性的UI很好，但清晰的帮助文档能让其锦上添花。

## 设计流程

* 理解需求并了解用户
    + 需求分析的工作一般由PM领导，主要由需求顾问完成。通过与用户访谈，旁观用户的工作，咨询行业专家或借鉴各类相关数据来得到用户场景。通过对用户场景的分组，过滤，以及挖掘，我们可以得到用户的角色以及不同角色对系统的需求。
    + 了解系统中的角色，以及他们之间的关系
        * 应该知道这些角色能够做什么，期望做些什么以及不能做些什么。
        * 要了解这些角色的主要任务，并深入研究他们的工作习惯、知识层次以及他们理想中的软件应该是什么样子。
        * 与这些代表不同角色的关键用户交谈，为他们每一个人编写一个场景来描述他们理想中的最佳体验是个不错的方法。作为设计者来说，我们必须清楚用户的习惯。在某些行业，可能从业者所希望的界面风格是常人无法理解的，但对于该角色确实是可行的。
    + 步骤
        * 与用户访谈，并记录用户描述，得到“访谈记录”。
        * 整理访谈记录，并得到“用户故事”。
        * 定义用户角色，得到“角色职责表”。
        * 定义用户权限，得到“权限列表”。
        * 定义用户场景，描述用户做什么，与系统如何交互，对出现的问题的反应，对系统的期望，得到“用户场景描述”。
    + 5W1H”，供读者借鉴。
        * What 用户要做什么？用户的期望是什么？
        * Why 用户的目标什么？用户为什么有这样的想法？
        * Where 用户处在何种场景活应用环境中使用系统？
        * When 用户什么时间使用这些功能？
        * Who 谁在使用这一系统？他们有什么差异？他们的习惯有何不同？
        * How 用户的业务流程是什么样的？系统如何帮助用户完成任务？
* 定义功能，划分模块
    + 业务流程是否清晰？
    + 数据流向是否清晰？
    + 数据字典（数据信息的定义）是否清晰？
    + 步骤
        * 分析用户场景，定义用例，得到“用例列表”、“用例图”。
        * 明确功能需求，得到“需求规格说明书”（仅功能需求部分）。
        * 划分模块，明确模块的功能，涉及的实体以及模块间的相互调用关系，数据流向，得到“功能结构图”、“模块设计说明书”或“概要设计”（仅UI部分）。
* 设计全局导航与局部导航:导航与标识的设计体现了设计者对复杂事物的组织能力
    - 导航与标识往往密不可分，很多时候导航就在充当标识。标识如同系统中的地标，帮助用户了解：他们身在何处，他们的目的地在哪，以及他们如何完成操做等。
    - 导航分类
        + 结构导航 结构导航显示了系统的层次结构，例如：全局导航。
        + 关联导航 关联导航用于将某个页面与和它有某种联系的页面相关联，例如：显示某项的详细信息。
        + 可用性导航 内容以外的所有功能导航都属于可用性导航，是系统功能非常重要的标识，其主要与某些功能页面相关联，例如：修改密码。
    - 导航模式
        + 弹跳 用户前往弄个子页面，需要先跳转到该子页面的父级或祖父级页面，然后逐级跳转到该页面。使用这个模式有两个原因——第一，有太多的层次或页面，用户可能需要一点点地沿着标识的路径达到目的地；第二，用户需要逐级与系统交互，确定路径走向。
        + 蟹行 用户像螃蟹行走一样，在页面之间横向跳转。该模式常常用于兄弟页面之间的跳转。
    - 步骤
        + 分析用户功能的实现逻辑，绘制“路径图”。
            * “用例图”和“系统结构图”都能反映出系统的功能结构。但是，它们都无法反映出用户如何使用系统。
            * “路径图”反映了用户如何使用系统，包含了业务逻辑，以及各功能模块之间的调用关系和数据流向。
            * “路径图”显示了用户完成任务，需要在系统中行走的路径，就如同地图一样，反映出不同功能的复杂程度。
        + 分解或合并功能模块。
            * 通过分析“路径图”，我们可以通过合并模块来将过程冗长的路径缩短，或者通过增加模块，更加详细地分解活动，实现更细粒度的控制和授权。但这一切的修改，都应该与关键用户共同来完成。
        + 设计导航栏。
            * 确定导航栏的位置 放在顶部可以增加内容区域的面积，但是导航条目过多时，一行就放不下了。放在左侧，可以增加导航栏的面积，可以放入比横行更多的按钮，但是会减少内容区域的面积。两者给有所长。需要根据需要选取。
            * 设计导航树 设计导航树要考虑两个问题。第一，导航树要适合进行权限控制。第二，导航树的层次要便于用户使用，一般常用功能的排列靠前，还有考虑树的深度，太深了会增加用户的记忆负担。
        + 确定局部导航的形式和规模。
            * 要确定局部导航的形式，可能的形式包括：包括在Logo中添加链接，在数据查询结果集中添加链接，“面包屑”等。
            * 确定局部导航的规模，局部导航过多会使系统路径相对复杂，增大开发工作量。因此，应该压低局部导航的数量，力争做到简单实用。
        + 动画设计。
            * 具有动画的导航具有更高的用户体验，而且对于数据需要延迟加载的导航来说，动画效果是必须的
            * 使用的场合要区别对待，并不是效果越绚丽越好。动画只需要流畅并能够个用户以反馈就好，毕竟对于应用系统而言，业务处理才是其核心价值，不能浪费项目组的宝贵资源来打造一个“花瓶”。
* 界面设计:最简单的方法就是参考同类系统的UI设计，结合实际项目和用户需要进行调整。界面设计有极大的自由度，因此也带来的一定的风险。设计者需要很强的业务知识，如果缺乏对用户工作的了解，很可能无法理解用户的真正期望
* 界面分割与整合
    - 从权限或功能复用角度将现有页面分块。
    - 按功能将所有块分组。
    - 分析每个分组中块间的共性与差异，结合每个块所包含实体的差异，来考虑该分组模块的可复用性。
    - 以分组为单位，抽象各个功能块，并作为整体UI的一块积木。
    - 使用新的UI分块来重组各个界面。
    - 在使用可复用组件组成的UI中，从包含的业务实体及数据传递角度重新考虑可行性。
    - 完成整体的迭代后，为各个功能块界面定义编号，并完整描述。
* 开发原型->演示->收集反馈->改进:以用户为中心设计系统的很重要的一步就是收集用户反馈。完成原型开发，并及时向用户演示，与用户频繁地交流，共同测试系统原型，能有效促成UI的高可用性。

| 问题      | 描述                                                                       | 解决方法                                          |
|:--------|:-------------------------------------------------------------------------|:----------------------------------------------|
| 少字段     | 这类错误经常在后期开发阶段才能发现，即便是使用原型向用户演示，常人也很难发现缺少某些数据。                            | 在设计界面时，就严格筛选界面包含的实体及其属性，考虑数据的收集和流向问题。         |
| 界面假死    | 当程序执行某个耗时的操作时，没有给用户以反馈，用户错误认为系统down掉了，此时有些用户不会耐心地等待系统反馈，而是以设计者难以预期的方式操作。 | 使用动画来提示用户系统“忙”。                               |
| 风格凌乱    | 当多位设计人员参与到界面设计时，容易发生风格不统一是事情，如样式差异，多种同义词，处理方式的不同等。                       | 约定规范，统一风格，由责任人负责统领全局。                         |
| 有去无回    | 某些操作完全是单向的，一旦进入无法返回，UI设计没有为用户提供相反的操作路径。                                  | 严格审核“路径图”。                                    |
| 歧义      | 同一界面中多个标识指向相同的位置，让用户感到迷茫。                                                | 减少不必要的局部导航。                                   |
| 无法实现    | UI设计人员不了解开发技术，错估技术难度，设计了超出成本或超过开发团队能力的界面。                                | 技术人员参与UI设计。                                   |
| 海量信息    | UI给用户呈现了过多的数据，让用户感觉到系统难以使用，并且极大地破坏系统的美观程度。                               | 优先“隐藏”而非“禁用”；展示用户期望的数据；分层次展示数据。               |
| 大量的手工输入 | UI没有帮助用户完成信息的采集，没有进行验证，也没有试图减少用户使用系统的工作量，造成用户在录入数据上过多地承担责任。              | 让系统尽力分担用户工作，减少用户使用系统时的工作量，并对用户信息进行验证，对错误进行提升。 |
| 缺少提示    | 用户在进行某些重要操作时，UI没有尽到提升义务，易造成用户使用时无意识地破坏数据。                                | 确认对话框。                                        |
| 臆测界面    | 设计人员从自己使用系统的角度出发来设计界面。由于缺少业务经验，往往会与用户期望发生偏差。                             | 沟通，沟通，以及沟通。                                   |
| 无序且没有重点 | UI的标识不明显，没有起到引导用户的作用，导航栏显得没有秩序，用户看不出当前界面有那些重点。                           | 为功能需求排序，常用功能应该得到更好的位置。                        |

## 设计图标

* 图形隐喻就是通过图形暗示用户的一种技巧。比如Windows里的回收站，历代Windows系列产品，只要看见那个“垃圾桶”就知道那是回收站。可见，好的UI，往往需要对图标进行定制化设计，使其包含某种隐喻来引导用户使用系统。
    - 图形隐喻可以推广到整个UI设计，不仅仅是图标设计，尤其是在游戏软件中。令我深有感触的就是《星际争霸II》，其UI设计无疑增加了游戏整体的用户体验。但是，使用图形隐喻存在一定风险。
    - UI设计者的个人看法，如果与大多数的人有偏差，就会适得其反。毕竟，做的仍然是应用软件而不是游戏，不会有强大的美工和设计团队，在我们追求前卫设计的时候，可能会让用户感到困惑。
    - 从风险和成本角度考虑，并不建议在应用软件中过多地依赖图形隐喻。也许，我们的软件没有什么特点，但作为应用软件UI，简约、易用、高效才是我们设计的目标。所以，在此我只考虑图标的设计原则。
* 图标设计的核心思想——用美观的图形抽象现实事务（事物）。以下是一些指导原则：
    - 图标风格应该保持一致，并且与系统UI相辅相成。
    - 图标应该提供清晰的标识，要选择合适的隐喻，例如回收站就用“垃圾桶”来隐喻。
    - 图标不会因文化而引起歧义。
    - 图标应该简单明了，应该保证用户可以看清。
    - 不要挑战用户的智商，直截了当的图标更受欢迎。
    - 图标的隐喻应该是约定俗成的，不应该修改那些普遍被大众所接受的方式，新的设计往往让用户迷惑。
    - 如果有行业的标准，如“播放”、“暂停”，就该墨守成规。

## 资源

* [花瓣](http://huaban.com/)
* [Canva](https://www.canva.com/):在线设计平台，预置了很多精美的模版，设计个海报什么的，分分钟的事儿，大大提好工作效率。在线设计绝对是个趋势，借助人工智能，设计的技术门槛肯定会越来越低，这时候，你的审美就越发重要
* [dribbble](https://dribbble.com/)
* [behance](https://www.behance.net/)：全球最优秀设计师的集中地，涵盖摄影、设计、插画等多个领域
* [Fwa](https://thefwa.com/):世界上最有创意，最优秀的网站和媒体艺术
* [Webby Awards](https://www.webbyawards.com/):互联网界的奥斯卡
* [lapa](http://www.lapa.ninja):优秀网站集合
* [Siteinspire](https://www.siteinspire.com/):收录了很多设计优秀网站，种类丰富，有产品、设计、摄影等
* [Adobe Spark Page]():在极短的时间内做出优雅炫酷的交互式网页
* [Nounproject](https://thenounproject.com/):非常优质的图标网站
* [Adobe color cc](https://color.adobe.com/):Aobe 旗下的配色网站，你可以在线配色，选择配色方案。不论是摄影还是设计，需要对颜色有足够的了解
* [Steller](https://steller.co/):展示自己的作品，比如摄影、绘画或其他创作，用 Steller 会显得特别优雅有格调
* [设计百宝箱](https://uirush.com/)
* [Arctime](http://www.arctime.org/):字幕制作神器
* [iconfont](http://iconfont.cn/)

## 硬件

* Wacom Folio

## web

* [frozenui](https://github.com/frozenui/frozenui)FrozenUI的CSS组件库,基于腾讯手Q样式规范 <http://frozenui.github.io/>
* [foundation-sites](https://github.com/zurb/foundation-sites):The most advanced responsive front-end framework in the world. Quickly create prototypes and production code for sites that work on any kind of device. <http://foundation.zurb.com>
* [design-blocks](https://github.com/froala/design-blocks):A set of 170+ Bootstrap based design blocks ready to be used to create clean modern websites. <https://www.froala.com/design-blocks>
* [Flat-UI](https://github.com/designmodo/Flat-UI):Flat UI Free - Design Framework (html/css3/less/js). Flat UI is based on Bootstrap, a comfortable, responsive, and functional framework that simplifies the development of websites. <https://designmodo.com/flat-free/>
* [airpal](https://github.com/airbnb/airpal):Web UI for PrestoDB. <http://airbnb.github.io/airpal>
* [Lona](https://github.com/airbnb/Lona):A tool for defining design systems and using them to generate cross-platform UI code, Sketch files, and other artifacts.
* [material-design-lite](https://github.com/google/material-design-lite):Material Design Components in HTML/CSS/JS <https://getmdl.io>
* [material-components/material-components-web](https://github.com/material-components/material-components-web):Modular and customizable Material Design UI components for the web <https://material.io/develop/>
* [vugu](https://github.com/vugu/vugu):Vugu: A modern UI library for Go+WebAssembly (experimental) <https://www.vugu.org>  <https://www.vugu.org/doc/start>

## Client

* [ant-design-mobile](https://github.com/ant-design/ant-design-mobile):A configurable Mobile UI <https://mobile.ant.design>
* [cube-ui](https://github.com/didi/cube-ui):A fantastic mobile ui lib implement by Vue <https://didi.github.io/cube-ui/>
* [OnsenUI](https://github.com/OnsenUI/OnsenUI):Mobile app development framework and SDK using HTML5 and JavaScript. Create beautiful and performant cross-platform mobile apps. Based on Web Components, and provides bindings for Angular 1, 2, React and Vue.js. <https://onsen.io/>
* [zui](https://github.com/easysoft/zui):ZUI is an HTML5 front UI framework. <http://zui.sexy>
* [weui](https://github.com/Tencent/weui):A UI library by WeChat official design team, includes the most useful widgets/modules in mobile web applications. <https://weui.io>
* [hotcss](https://github.com/imochen/hotcss):移动端布局终极解决方案 --- 让移动端布局开发更加容易 <http://imochen.github.io/hotcss/>
* [](https://github.com/ydcss/vue-ydui) A mobile components Library with Vue2.js http://vue.ydui.org/

* [vux](https://github.com/airyland/vux):Mobile UI Components based on Vue & WeUI <https://vux.li/>
* [vuetify](https://github.com/vuetifyjs/vuetify):Material Component Framework for Vue.js 2 <https://vuetifyjs.com>
* [vue-material](https://github.com/vuematerial/vue-material):Material design for Vue.js <http://vuematerial.io>
* [Keen-UI](https://github.com/JosephusPaye/Keen-UI)
* [Buefy](https://github.com/buefy/buefy)
* [at-ui](https://github.com/at-ui/at-ui):A fresh and flat UI-Kit specially for desktop application, made with ♥ by Vue.js 2.0 <https://at.aotu.io>
* [muse-ui](https://github.com/museui/muse-ui):Material Design UI library for Vuejs 2.0 <https://museui.github.io>
* [iview](https://github.com/iview/iview):A high quality UI Toolkit built on Vue.js 2.0 <https://iviewui.com/>
* [Uiv](https://github.com/wxsms/uiv)
* [Semantic UI+Vue](https://semantic-ui-vue.github.io/)
* [Fish-UI](https://github.com/myliang/fish-ui)
* [mint-ui](https://github.com/ElemeFE/mint-ui/):Mobile UI elements for Vue.js <http://mint-ui.github.io/#!/en>
* [Framework7 Vue](https://framework7.io/vue/)
* [Vueblu](https://github.com/chenz24/vue-blu)
* [Ant Design Vue](https://github.com/okoala/vue-antd)
* [vant](https://github.com/youzan/vant):Lightweight Mobile UI Components built on Vue <https://youzan.github.io/vant>
* [bootstrap-vue](https://github.com/bootstrap-vue/bootstrap-vue/):BootstrapVue provides one of the most comprehensive implementations of Bootstrap 4 components and grid system for Vue.js and with extensive and automated WAI-ARIA accessibility markup. <https://bootstrap-vue.js.org>
* [Eagle.js](https://github.com/Zulko/eagle.js)
* [nutui](https://github.com/jdf2e/nutui):京东风格的轻量级移动端Vue组件库 (A Vue.js 2.0 UI Toolkit for Mobile Web) <https://nutui.jd.com>
* [HEYUI](https://www.heyui.top/):基于Vue.js的高质量UI组件库

## 工具

* [Brackets](http://brackets.io/):A modern, open source text editor that understands web design.
* [lepton](https://github.com/dropbox/lepton):Lepton is a tool and file format for losslessly compressing JPEGs by an average of 22%.
* [Figma](https://www.figma.com/):在线工具
  - [使用 Figma + GitHub Actions 完成 SVG 图标的完全自动化交付](https://sspai.com/post/61182)
* [botui](https://github.com/botui/botui):🤖 A JavaScript framework to create conversational UIs <https://botui.org>
* [wired-elements](https://github.com/wiredjs/wired-elements):Collection of elements that appear hand drawn. Great for wireframes. <https://wiredjs.com>
* [ice](https://github.com/alibaba/ice/):🚀 飞冰 - 让前端开发简单而友好，海量可复用物料，配套桌面工具极速构建前端应用，效率提升 100% <https://alibaba.github.io/ice/>
* [CosmicMind/Material](https://github.com/CosmicMind/Material):A UI/UX framework for creating beautiful applications. <http://cosmicmind.com>
* [happo](https://happo.io/)
* [imgcook](https://imgcook.taobao.org)
* [设计工具](https://www.canva.cn)
