# Project Manager PM

* Communicate project vision, business objectives, scope and priorities to the project team and relevant stakeholders
* Represent the team in stakeholder meetings
* Create and maintain a communication plan
* Identify, track and mitigate project risks and issues in collaboration with Iteration Manager and relevant stakeholders
* Ensure development and maintenance of the deployment strategy – CI, environments, integration, UAT, data migration, production deployment, production support etc.
* Ensure development and maintenance of the test strategy – functional automation, performance, security, etc in appropriate environments
* Ensure that scope is effectively managed by the Business Analyst(s), Iteration Manager and Product Owner
* Assist with Release Planning based on agreed scope and priorities
* Manage budget and resources (capacity)
* Track and communicate project status / progress with stakeholders and the team
* Remove obstacles that can affect project timelines (e.g. hardware, tools, resource constraints)
* Track external dependencies across projects and teams – these will include other development teams as well as areas like infrastructure and environments.
* Keep the management as agile and as lightweight as possible

## 责任

* 要负责统筹规划项目进度及产品生命，其工作职能直接对公司高层负责
* 即在有限的资源约束下，运用系统的观点、方法和理论，对项目涉及的全部工作进行有效地管理
* 团队里的每个人都不好管，而且每个人都认为自己不需要被管理（当然这种想法在大多都是错误的)
* 需要和客户快速建立信任，并推动项目进入正轨
* 需要了解大量与项目相关的上下文（业务上下文，人员关系，资源协调等）
* 识别所有的项目风险，然后不断跟进
  - 技术风险
  - 资源风险
* 在项目之初将项目范围定下来，这个范围的划分非常依赖经验
  - 划得少了团队得天天加班，累得跟狗一样才能保证交付（据我的经验，虽然项目一般不会天天加班，但是总会有一些攻关、打补丁的事儿，最后还是会累成狗）
  - 划得多了客户不买单，意思是就这个小功能你要做两个月，绝对不行
* 察言观色
  - 在showcase的时候，有个客户说，“嗯，挺好，整个流程就是这样的，后续你们的UI是不是还会美化
    + 先判断，提出这个问题的人是什么角色，以及他在系统中的话语权如何
    + 还有其他人就此问题的反应如何等，然后找到一个合适的答案
* 扯皮
  - 释放团队中的负面情绪，保证团队士气，还需要做一些开发不屑于做的琐碎事情
* 作为开发
  - 不要因为一个人不会某个技术而鄙视他
  - 学习如何报告进度
    + 站会前自己花3分钟整理一下昨天做的工作
    + 根据story的验收条件（最好有和BA/QA一起的讨论需求），进行合理的任务划分（tasking技能）
    + 可以借助便签纸等工具，帮助自己明确进度（划分了5个子任务，昨天完成了3个，那么可以粗略的估计为60%）
  - 合理估算
    + 明确告诉PM，有哪些需求是不可能按时交付的，PM会根据实际情况来重新定计划，并和客户确认
    + 明确告诉PM一些可能的风险，团队整体对交付负责，而不是PM，或者开发

## 项目

* 客户细分：所服务的客户群体、⼲系人
* 价值主张：项⽬或服务的特殊价值，差异点
* 关键业务：确保⽬标达成做的重要事情
* 渠道通路：如何接触客户 /⼲系人传递主张成果
* 客户关系：团队和客户建立和维持什么样的关系
* 重要伙伴：让项⽬有效运作需要的伙伴或者支持
* 核⼼资源：保证项⽬结果产出需要的最重要的资源
* 成功目标：项⽬成功希望达成或收获的目标
* ⻛险和机遇：不确定性，可能存在的风险或者机遇

## 活动
* 拉
  - 做计划，带团队交付
  - 培养人
* 推
  - 组织会议，跟踪⾏动
  - 监督指导

## [产品需求分析](https://insights.thoughtworks.cn/product-requirement-analysis/)

* 工作流系统
  - 横切：先切分出工作流中核心且轻薄的一层，然后再去实现各个步骤中的细节部分
    + 对于那些核心业务逻辑比较简单、但每个步骤的附属功能多且复杂的工作流系统来说比较适用
    + 不影响本步骤走通的情况下，最小化这个步骤的工作量，加速打通整个业务流程
    + 优势在于可以快速实现核心逻辑，并快速上线，验证假设并收集反馈，可以根据反馈的结果来决定每个步骤中的功能应该如何设计、优先级是什么，来避免一些可能出现的浪费
    + 缺点在于整个工作流设计会采用短平快的原则，用户体验较差
  - 纵切：按照工作流中的每一个步骤进行切分，这样可以使每一个步骤都具有相对完善的功能，这在某些需要关注终端用户交互体验的产品中应用较多
    + 如果在整个工作流中，需要跟终端用户进行交互的功能仅出现在某几步中，如第一步和最后一步，而中间的N-2步都是后台流程，在开发中，可以先实现第一步和最后一步的功能，而中间的流程处理环节，仍然采用逐步线上化的方式，这样可以使整个工作流系统最快的上线，同时能平衡用户的交互体验
    + 这几个步骤拆出来优先实现，及早上线；而中间的跟票务相关的步骤，仍然采用线下的形式
    + 对于一些流程复杂但用户量较小的初创公司比较适用，可以在保证用户体验的情况下，大大提升产品上线速度，并降低试错成本
  - 不管是横切还是纵切，工作流中的每一个步骤都会遵循80/20法则，也就是20%的功能决定了这个步骤的核心价值，而80%的功能仅仅是锦上添花的，所以我们需要更深刻地研究客户的真正需求是什么，提炼出这20%的业务价值到底在哪里，从而进行更加合理的拆分
* 功能模块拆分
  - 按业务规则拆分：典型例子是搜索引擎，输入框只有一个，会根据所输入的数据规则的不同，来进行不同的处理操作
    + 可以把每一个业务规则都单独拆分成一个用户故事
    + 虽然这些用户故事看起来很相似，但是大部分情况下，这些规则的优先级是截然不同的。总会有一簇最高优先级的用户故事以及围绕在外围的用户故事
  - 1+N模式：对同样一个流程，在终端接不同的网关或渠道。最典型的例子是在线支付
    + 第一次实现支付的功能，可能会比较复杂，但后面如果从一种扩充到多种支付方式，就相对比较简单
    + 最先需要支持什么样的支付方式，可能在一开始也拿不定主意。这个时候，我们不妨将支付功能拆成2张卡
      * 会员可以使用微信支付/京东支付/网银支付中的一种进行支付
      * 会员可以使用微信支付/京东支付/网银支付三种渠道进行支付
    + 可以延迟决策-我们需要最先支持哪种支付方式，同时合理的评估项目的工作量
* 复杂业务模型拆分
  - 非常复杂的业务模型，如果一上来就要考虑清楚这个业务模型的方方面面，是个性价比很低的事情——做了很多功课，但没有给客户带来真正的业务价值
  - 区分哪些信息是核心信息，是对用户来说最有价值的，把这些信息从业务模型中提取出来，而后设计相应的更小的业务功能，切忌一蹴而就
  - 将业务模型，按照实际需要提供功能进行拆分。比如，要做一个中介搜索系统，可以仅取出模型中的中介信息，而不需要处理其它部分。即使需要整个业务模型去做一些事情，也可以把其拆成一个个子模型，根据子模型的业务价值及优先级去设计相应的功能
* 需求拆分是没有银弹的，要根据具体的场景、限制来选择合适的拆分方法。在遇到使用某个拆分方法，不能满足当前业务需求时，看看是不是可以换个思路，换个方法，在选择拆分方法时，也有一些技巧
  - 基于80/20法则，选择那些可以拆出低优先级卡片（或者可以被扔掉的卡片）的拆卡法。
  - 选择可以把卡片拆的大小差不多的方法，未来在发布计划中更容易做需求置换
  - 选择开发团队更容易理解和实现的方式
* 反模式
  - 按照技术架构分层进行拆分，常见的会按照持久层、应用层、展示层进行拆分。这种拆分方式拆出来的用户故事，会明显破坏INVEST中的Valuable的原则，而且各个故事卡由于各方面的原因，如开发进度不统一，无法灵活的集成上线
  - 拆分时，把复杂的UI交互算在故事卡片中。大部分情况下，比较fancy的UI交互都不是核心的业务功能，这部分功能可以作为用户体验优化的卡片，独立拆出来
  - 拆分时，过早考虑性能问题。在性能基本达标、不出现大问题的情况下，提升性能很多情况下也属于用户体验的一部分，可以单独拆出来，左右优化卡片
  - 拆出一些管理类的卡片。比如管理产品，实际上可能包含很多产品相关的操作，如导入、编辑、同步信息、改变状态、上架、下架等，所以应该根据具体的功能，拆分成更为准确和大小合适的故事卡片

## 用户故事 User Story

* 用户故事描述了客户或用户如何使用产品，从用户的角度进行表达。另外，用户故事特别有助于捕捉特定的功能。首先进行必要的用户研究，否则，就有基于自己的想法和信念写出假想的故事的风险，而不是基于数据和经过验证的证据。
* 使用角色来发现正确的故事：人物角色是基于目标群体的第一手知识的虚构人物。他们通常由一个名字和一张照片组成，还包括相关的特征、行为和态度、以及一个目标。目标是人物想要获得的利益，或者人物想要通过使用产品来解决的问题
  - 人物角色的目标可以帮助你发现正确的故事：问问自己，为了达到人物角色的目标，产品应该提供什么样的功能。正如我在“ 从角色到用户故事” 的文章中解释的那样。可以从romanpichler.com/tools/persona-template下载一个方便的模板来描述您的角色
* 合作创作故事：用户故事旨在作为一种轻量级的技术，而是一个协作工具。故事不应该交给开发团队。相反，他们应该被嵌入到一个对话中：产品负责人（PO）和团队应该一起讨论这些故事。这使您只能捕获最少量的信息，减少开销并加速交付。让团队协作来写故事，这可以是产品backlog梳理过程中的一个环节。如果你不能让开发团队参与用户的故事工作，那么你应该考虑使用另一种更正式的技术来捕获产品功能，例如用例
* 保持故事简单和简洁：避免混淆和模棱两可的条款，并使用主动语态。专注于重要的东西，而忽略其余的东西 作为<persona>, 我想要<what？> 以便<why？>。
* 从Epics开始：史诗是一个大而粗略，粗糙的故事。它通常会随着时间的变迁而分解成多个用户故事 – 基于用户对早期原型和产品增量的反馈。你可以把它看作是一个标题和一个更详细的故事的占位符
  - 从史诗故事开始，能够让你在不关注太多产品详细信息的情况下捕获产品的功能。这对于描述新的产品和功能特别有帮助：它可以让您捕捉到粗略的范围，这节省了你了解如何最好地满足用户的需求的时间。
  - 也减少了整合新想法所需的时间和精力。如果在产品Backlog中有很多详细的故事，那么将反馈和对应的条目关联起来往往是非常棘手和耗时的，并且还有导致信息不一致的风险。
* 细化故事，直到准备就绪：把史诗分成更小，更详细的故事，直到准备就绪：清晰，可用，可测试。所有的开发团队成员应该对故事的意义有一个共同的理解; 这个故事不应该太大且能放到一个Sprint，还必须有一个有效的方法来确定故事是否完成
* 添加验收标准（AC）：把史诗分成更小的故事时，请记住添加验收标准。验收标准补充叙述：它们用来描述故事达到完成必须完成的条件。验收标准丰富了故事，使其成为可测试的，并确保故事可以演示或发布给用户和其他干系人
* 使用纸卡：用户故事出现在极限编程（XP）中，早期的XP文献讲述了故事卡而不是用户故事。有一个简单的原因：用户故事被捕获在纸卡上。这种方法提供了三个好处：首先，纸卡便宜且易于使用。其次，他们促进合作：每个人都可以拿一张卡片并记下一个想法。第三，卡片可以很容易地分组在桌子或墙上，以检查一致性和完整性，并可视化依赖关系。即使你的故事是以电子方式存储的，当你写新的故事时，使用纸卡也是值得的。
* 保持你的故事可见和可访问：故事要传达信息。因此，不要将其隐藏在你的服务器和电脑上。可以把它们放在墙上，使它们可见。这会促进协作，创建透明度，而且可以很快的发现过快地添加了太多的故事，因为的墙面快用完了。有一个方便的工具可以帮助你来发掘、可视化和管理你的故事，这就是我的产品画布
* 不要单靠用户故事：创造出色的用户体验（UX）需要的不仅仅是用户故事。用户故事有助于捕捉产品功能，但不能很好地描述用户旅程和视觉设计。因此，可以用其他技术来补充用户故事，例如故事地图，工作流程图，故事板，草图和模型

* 敏捷开发的基础，从用户的角度来对需求进行描述。软件开发是为了实现产品的商业价值，满足用户需求。只要需求足够明确，所有人都了解其具体内容，团队就能简单有效地把需求转化成可实现、可测试、能够发布的代码
* 定义
  - A tool for iterative development
  - Represents a unit of work that should be developed
  - Help track that piece of functionality;s lifecycle
  - It is a token for a conversation , a placeholder for a conversation
* 作用
  - 用于需求描述
  - 促进共同理解
* Story Card
  - A conversation placeholder, not a detailed requirements document
  - Designs may be needed for a story before it is ready for development
  - Focus on the user,their goals and the value they seek
  - Mock ups are a low-fi sketch that convey story concept and prompt early feedback
  - NARRATIVE: Describes the purpose of a story
  - ACCEPTANCE CRITERIA: describe the requirements to complete a card: Given when That
  - Structure
    + Biz Value
    + Description
    + Hi-fi/low-fi Mockup
    + ACCEPTANCE CRITERIA
* 用户故事开卡 Story kick-off
  - 在每个用户故事开发之前，要确保BA、DEV和QA对用户故事理解一致
  - 这个沟通活动通常表现为由DEV讲解这个用户故事要完成的功能及AC，一旦发现任何疏漏，BA及时补充
  - DEV有任何疑惑也需及时提出来，当场确认，使这些功能得以正确实现
  - 在后续开发中如果碰到任何疑惑，也应及时找BA了解清楚。QA会严格按照AC来验收用户故事
* 怎么写
  - 要素
    + 角色：谁要使用这个功能
    + 活动：需要完成什么样的功能
    + 商业价值：为什么需要这个功能，这个功能带来什么价值
  - 角色:从系统中的角色出发，沿着User Journey梳理用户故事。细分角色，比如一个育儿社区应用，用户可以有爸爸，妈妈，爷爷奶奶等，他们需求和痛点可能是不一样的
  - 格式:`As a ... I want ... So that ...` 作为一个< 某种类型的用户角色>，我要< 达成某些目的>，只有这样我才能够获取< 商业价值>
    + 原来描述需求时，基本只有中间的功能部分。不提这个功能是为谁做的，需求不明确时，不知道该找谁确认，功能上线后，不知道找谁要反馈。也不提满足了用户的什么价值，做出来也没有用户去用
  - 原则
    + 3C原则
      * Card，用粗笔将 User Story 写到物理卡片上，用粗笔是强迫不能写太多太详细，促进当面沟通
      * Conversation，Dev 会拿着卡去找 BA 和 QA 讨论
      * Confirmation，讨论完要确认验收条件
    + INVEST模型：Bill Wake提出了一个好用户故事的验收标准
      * Independent：每个用户故事应该是独立的，不会和其他用户故事产生耦合.如果用户故事存在依赖性那么就会导致用户故事之间存在着不同的优先级，只有被依赖的用户故事完成才能继续开发依赖的用户故事。一般可以通过组合用户故事或者分割用户故事来减少用户故事间的相互依赖性。
      * Negotiable：并不会非常明确的阐述功能，细节应带到开发阶段跟程序员、客户来共同商议
      * Valuable：每一个用户故事的交付都要能够给用户带来用户价值,因此应该站在用户的角度去编写，描述的是一个一个的feature，而非一个一个的task
      * Estimable：最直观的判断就是看它能不能被估算。如果很难估算，要么是故事没有描述清楚，要么是这个故事太大
      * Small：要小一点，但不是越小越好，短小的故事可以减少划分过程中估算的误差，最好的故事是能够在一个迭代周期之内完成的。如果太大就应该考虑将其拆分为多个粒度更小的用户故事
      * Testable：需要能够进行验收测试，最好能把Test Case提前加进去
        - 对应的验收测试也最好是自动运行的
        - 必须在定义了验收测试通过的标准后才能认为故事划分完毕
  - 用户故事一旦被确定，那么所要实现的功能、需求范围、所需工作量也就随之确认了。之后开发人员所要做的就是根据这个用户故事的内容进行开发，只有当所有Acceptance Criteria 被覆盖到，测试人员完成测试，发现所有功能是可测试的、可运行的，这个用户故事才算完成了
  - 准备
    + 开始写共识之前，先完成用户体验地图和人物形象构建是很有用的。从产品草图开始也一样
    + 做准备时，确保准备好卡片、马克笔、和大面的墙以及排卡片时需要的大桌子
    + 确保产品负责人和团队都参与写故事，对于大型团队，考虑组成小队，并分别专注于用户体验的不同部分
  - 对于API卡，两点建议
    + 从User Story描写的角度，“As a ” 这个User可以是一个Persona，也可以是第三方的系统。比如说“As e-Comm Digital web app, I want to call Customer API to retrieve customer details”.
    + 最适合用GIVEN WHEN THEN的方式来定义AC
      * GIVEN a customer exists
      * WHEN a GET request of Customer API is made
      * THEN Customer Name, Contact Details, Product Details are returned in the response.
* Check
  - Simple to understand
  - Testable
  - Estimable
  - Has Business Value
  - Can be aimed in an iteration (timebox)
  - Understandable by the user
* [如何拆分](https://insights.thoughtworks.cn/product-requirement-analysis/)
* 如何划分优先级
  - ![moscow](../_stataic/moscow.png "Optional title")
  - ![private metrics](../_stataic/private_metrics.png "Optional title")
  - ![story mapping](../_static/story_mapping.png "Optional title")
* 估算:相对估算
  - ![estimation](../_static/estimation.png "Optional title")
* 非功能性需求
  - ![cross functional requirements](../_staic/cross_functional_requirements.png "Optional title")
* 交付管理
  - ![Why just in time](../_staic/story_in_time.png "Optional title")
  - ![story's lifecycle](../_static/lifecycle__of_story.png "Optional title")
  - ![需求层次](../_static/product_level.png "Optional title")
* 什么是好的Story,几个反模式
  - 按照技术架构分层进行拆分，常见的会按照持久层、应用层、展示层进行拆分。这种拆分方式拆出来的用户故事，会明显破坏INVEST中的Valuable的原则，而且各个故事卡由于各方面的原因，如开发进度不统一，无法灵活的集成上线。
  - 拆分时，把复杂的UI交互算在故事卡片中。大部分情况下，比较fancy的UI交互都不是核心的业务功能，这部分功能可以作为用户体验优化的卡片，独立拆出来。
  - 拆分时，过早考虑性能问题。在性能基本达标、不出现大问题的情况下，提升性能很多情况下也属于用户体验的一部分，可以单独拆出来，左右优化卡片。
  - 拆出一些管理类的卡片。比如管理产品，实际上可能包含很多产品相关的操作，如导入、编辑、同步信息、改变状态、上架、下架等，所以应该根据具体的功能，拆分成更为准确和大小合适的故事卡片

![Alt text](../__static/3c.png "Optional title")

## 故事点 Story Point

* 一个度量单位，用于表示完成一个产品待办项或者其他任何某项工作所需的所有工作量的估算结果
* 为每个待办项分配一个点数。待办项估算结果的原生数据并不重要，只关注最后得到的相对估算结果。一个估算值为2的用户故事应该是估算值为1的用户故事的2倍。而也应该是另一个估算值为3的用户故事的三分之二
* 团队不要采用100、200、300，或者1百万、2百万、3百万，而要使用1、2、3。估算结果是比值，而不是绝对值
* 内容：代表了开发用户发故事所需的全部工作量，所以团队的估算必须考虑到影响工作量的所有因素。这可能包括
  - 要开展的工作的数量（The Amount of Work）
  - 工作复杂度（Complexity）
  - 要开展的工作中存在的任何风险或不确定性（Risk and Uncertainty）
* 故事点估算必须要覆盖直到实现产品待办项待真正完成的所有事项。如果团队的“完成的定义”中包括了创建自动化测试来验证这个故事（并且这是一个好主意）这个事项，那么创建这些测试的工作量也应该包含在故事点估算结果中

## 跨功能需求 Cross-Functional Requirements, CFR

## 非功能需求 Non-Functional Requirements NFR

* In systems engineering and requirements engineering, a non-functional requirement (NFR) is a requirement that specifies criteria that can be used to judge the operation of a system, rather than specific behaviors. They are contrasted with functional requirements that define specific behavior or functions. The plan for implementing functional requirements is detailed in the system design. The plan for implementing non-functional requirements is detailed in the system architecture, because they are usually architecturally significant requirements.
* Broadly, functional requirements define what a system is supposed to do and non-functional requirements define how a system is supposed to be. Functional requirements are usually in the form of “system shall do “, an individual action or part of the system, perhaps explicitly in the sense of a mathematical function, a black box description input, output, process and control functional model or IPO Model. In contrast, non-functional requirements are in the form of “system shall be “, an overall property of the system as a whole or of a particular aspect and not a specific function. The system’s overall properties commonly mark the difference between whether the development project has succeeded or failed.
* Non-functional requirements are often called “quality attributes” of a system. Other terms for non-functional requirements are “qualities”, “quality goals”, “quality of service requirements”, “constraints”, “non-behavioral requirements”, or “technical requirements”. Informally these are sometimes called the “ilities”, from attributes like stability and portability. Qualities—that is non-functional requirements—can be divided into two main categories:
		- Execution qualities, such as safety, security and usability, which are observable during operation (at run time).
		- Evolution qualities, such as testability, maintainability, extensibility and scalability, which are embodied in the static structure of the system.
