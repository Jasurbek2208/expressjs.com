---
layout: page
title: 为快递做贡献
description: 了解如何对 Express.js 做出贡献，包括报告问题、提交合并请求、成为合作者以及了解安全政策。
menu: resources
lang: 中
redirect_from: ""
---

# 为快递做贡献

### 想要对 Expressjs.com做贡献吗？ Click [here](#expressjs-website-contributing).

Express和[在 GitHub 上的 Expressjs 组织](https://github.com/expressjs)中的其他项目是[OpenJs 基金会](https://openjsf.org/)的项目。
这些项目根据诺德.js基金会的一般政策和准则以及下面的补充准则进行管理。

- [Technical committee](#technical-committee)
- [Community contributing guide](#community-contributing-guide)
- [Collaborator's guide](#collaborators-guide)
- [Security policies and procedures](#security-policies-and-procedures)

## 技术委员会

快递技术委员会由现任项目成员组成，并指导快递项目的开发和维护。 For more information, see [Express Community - Technical committee](community.html#technical-committee).

## 社区贡献指南

<!-- SRC: expressjs/express Contributing.md -->

本文件的目标是建立一个贡献过程：

- 5. 鼓励提供新的捐款。
- 4. 鼓励捐助者继续参与。
- 尽可能避免不必要的过程和官僚作风。
- 创建一个透明的决策过程，明确
 贡献者如何参与决策。

### 词汇表

- **贡献者** 是任何个人创建或评论一个问题或拉取请求。
- **Committer** 是被授予对资源库的写权限的贡献者的子集。
- **Project Captain** 是仓库的主要维护者。
- **TC (技术委员会)** 是一个代表解决稀有争端所需的技术
 专门知识的承诺者。
- **Triager** 是被授权访问仓库的贡献者的子集。

### 日志问题

记录您可能遇到的任何问题或问题。 当有疑问时，记录一个问题和
将在答复中提供任何关于应包括哪些内容的额外政策。 唯一的
例外是应私下发送的安全披露。

Committers may direct you to another repository, ask for additional clarifications, and
add appropriate metadata before the issue is addressed.

请礼节和尊敬。 每个参与者都要遵守
项目的行为守则。

### 二. 捐款

这个资源库中的任何更改必须通过拉取请求。 这适用于文档、代码、二进制文件等的所有更改
。 即使是长期承诺者和技术合作成员也必须使用
拉取请求。

不正在审核，任何拉取请求都不能合并。

对于非微不足道的贡献，拉取请求应至少36小时，以确保其他时区的
贡献者有时间审查。 Consideration should also be given to
weekends and other holiday periods to ensure active committers all have reasonable time to
become involved in the discussion and review process if they wish.

对每笔捐款的默认情况是，一旦没有任何委员会表示反对，就会被接受。
在审查过程中， 提交者还可以请求一个特定的
特定区域的特定贡献者在合并之前提供“LGTM ”。 没有额外的 "注销"
进程用于对土地的贡献。 Once all issues brought by committers are addressed it can
be landed by any committer.

In the case of an objection being raised in a pull request by another committer, all involved
committers should seek to arrive at a consensus by way of addressing concerns being expressed
by discussion, compromise on the proposed change, or withdrawal of the proposed change.

如果捐款有争议，而且承诺方不能就如何让它进入
土地或是土地上达成一致，那么就应该将它升级到TC。 TC members should regular
discussion pending contributions in order to resolution 预计只有少数
问题提交技术合作理事会解决，而承诺国之间的讨论和
是默认解决机制。

### 成为一个三角龙者

任何人都可以成为一个试验者！ Read more about the process of being a triager in
[the triage process document](https://github.com/expressjs/express/blob/master/Triager-Guide.md).

Currently, any existing [organization member](https://github.com/orgs/expressjs/people) can nominate
a new triager. 如果您有兴趣成为一个三角龙， 我们最好的建议是通过帮助试用问题和拉取请求来积极参与
的社区。 我们也建议
参与其他社区活动，例如参加技术合作会议和参加Slack
讨论。 If you feel ready and have been helping triage some issues, reach out to an active member of the organization to ask if they'd
be willing to support you. 如果他们同意，他们可以创建一个拉请求来使您的提名正规化。 如有人对提名提出异议，则由甄别小组负责与有关个人合作并寻找解决办法。

如果您有问题或需要指导，您也可以联系任一[组织成员](https://github.com/orgs/expressjs/people)
。

### 成为一个委员会

所有作出了重要和宝贵贡献的捐助国都应及时参与。
并添加为提交人，并被授予对资源库的写权限。

预计提交者将遵循此政策并继续发送拉取请求。 通过
进行适当的审查，让其他提交者合并他们的合并请求。

### TC 进程

技术合作机构对升级到技术合作机构的问题使用“寻求共识”进程。
该小组试图找到一项在技术合作组织成员之间没有公开反对意见的决议。
如果不能达成没有反对意见的共识，那么就要求多数票获得
还预期技术合作理事会作出的大多数决定都是通过
寻求共识的过程，而表决只是作为最后手段使用。

Resolution may involve returning the issue to project captains with suggestions on
how to move forward towards a consensus. It is not expected that a meeting of the TC
will resolve all issues on its agenda during that meeting and may prefer to continue
the discussion happening among the project captains.

成员可以随时加入TC。 Any TC member can nominate another committer
to the TC and the TC uses its standard consensus seeking process to evaluate whether or
not to add this new member. 技术合作委员会将由至少3名现任成员和最多10名
成员组成。 如果TC 应该掉落到5个成员以下，则活跃TC 成员应该提名
个新成员。 如果一个技术合作成员正在退出，他们会被鼓励(但不需要)
提名他人接替他们。

TC 成员将被添加为 Github orgs, npm orgs 的管理员和其他资源为
以有效地发挥这一作用。

要保持“活跃”，技术合作成员应在过去12个月内参加，并且错过
最多连续六次技术合作会议。 我们的目标是增加参与，而不是因为没有参与而惩罚
人。 此准则只能用作
(例如用新的活跃成员取代不活跃成员)。 不符合此
的成员预计会下调。 如果一个TC 成员没有下调，可以在
讨论中打开一个问题，将它们移动到非活动状态。 由于
故障，TC 成员下调或被移除，将被移到非活动状态。

非活动状态成员可以通过自我提名成为活跃成员，如果TC 还不是
大于最多10。 如果
活动成员在最大尺寸时下调，他们也会被优先考虑。

### 项目队长

Express TC可以为
组织的个别项目/仓库指定船长。 这些船长负责技术和社区阵线上
公司的主要日常维护者。
Repo上尉有权拥有repo所有权和包裹出版权。
当发生冲突，特别是在影响快递项目
的主题上发生冲突时， 船长负责将其提升到技术合作公司，并促使
这些冲突得到解决。 警长还负责确保
社区成员遵守社区指导方针。 保留Repo
和已发布的软件包，以及提供用户支持。

像TC 成员一样，Repo 上尉是一个子集的提交者。

为了成为一个项目的船长，候选人将在申请之前作为委员会至少6个月参加这一
项目。 They should have
helped with code contributions as well as triaging issues. They are also required to
have 2FA enabled on both their GitHub and npm accounts.

任何TC 成员或在 **相同** 的现有船长都可以提名另一个
委员会担任船长。 为此，它们应向本文件提交一份项目报告。 更新
**Active Project Captains** 部分 (同时保持排序顺序) 包含项目
名称 被提名人的GitHub 手势以及他们的 npm 用户名(如果不同的话)。

- 仓库可以有尽可能多的船长对工作范围有意义。
- 技术合作成员或现有的技术合作项目船长**在同一个项目上**可以提名一个新的船长。
 来自其他项目的Repo船长不应为另一个项目指定船长。

PR 将需要至少2个技术合作成员的批准和2个星期的时间才能允许
发表评论和/或表示异议。  当PR 被合并时，TC 成员会将他们添加到
合适的GitHub/npm 组。

#### 活动项目和船长

- [`expressjs/badgeboard`](https://github.com/expressjs/badgeboard): @wesleytodd
- [`expresjs/basic-auth-connect`](https://github.com/expressjs/basic-auth-connect)：@ulisesGascon
- [`expresjs/body-parser`](https://github.com/expressjs/body-parser)：@wesleytodd、@jonchurisch、@ulisesGascon
- [`expresjs/compression`](https://github.com/expressjs/compression)：@ulisesGascon
- [`expressjs/connect-multiparty`](https://github.com/expressjs/connect-multiparty): @ulisesGascon
- [`expressjs/cookie-parser`](https://github.com/expressjs/cookie-parser): @wesleytodd, @UlisesGascon
- [`expresjs/cookie-session`](https://github.com/expressjs/cookie-session)：@ulisesGascon
- [`expressjs/cors`](https://github.com/expressjs/cors): @jonchurch, @ulisesGascon
- [`expresjs/discussions`](https://github.com/expressjs/discussions)：@wesleytodd
- [`expressjs/errorhandler`](https://github.com/expressjs/errorhandler): @ulisesGascon
- [`expressjs/express-paginate`](https://github.com/expressjs/express-paginate): @ulisesGascon
- [`expressjs/express`](https://github.com/expressjs/express): @wesleytodd, @ulisesGascon
- [`expressjs/expressjs.com`](https://github.com/expressjs/expressjs.com): @crandmck, @jonchurch, @bjohansebas
- [`expresjs/flash`](https://github.com/expressjs/flash)：@ulisesGascon
- [`expressjs/generator`](https://github.com/expressjs/generator): @wesleytodd
- [`expressjs/method-override`](https://github.com/expressjs/method-override): @ulisesGascon
- [`expresjs/morgan`](https://github.com/expressjs/morgan)：@jonchurch, @ulisesGascon
- [`expressjs/multer`](https://github.com/expressjs/multer): @LinusU, @ulisesGascon
- [`expresjs/response-time`](https://github.com/expressjs/response-time)：@UlisesGascon
- [`expressjs/serve-favicon`](https://github.com/expressjs/serve-favicon): @ulisesGascon
- [`expresjs/serve-index`](https://github.com/expressjs/serve-index)：@ulisesGascon
- [`expresjs/serve-static`](https://github.com/expressjs/serve-static)：@ulisesGascon
- [`expresjs/session`](https://github.com/expressjs/session)：@ulisesGascon
- [`expressjs/statusboard`](https://github.com/expressjs/statusboard): @wesleytodd
- [`expressjs/timeout`](https://github.com/expressjs/timeout): @ulisesGascon
- [`expressjs/vhost`](https://github.com/expressjs/vhost): @ulisesGascon
- [`jshtp/accepts`](https://github.com/jshttp/accepts)：@blakeembrey
- [`jshttp/basic-auth`](https://github.com/jshttp/basic-auth): @blakeembrey
- [`jshttp/compressible`](https://github.com/jshttp/compressible): @blakeembrey
- [`jshttp/content-disposition`](https://github.com/jshttp/content-disposition)：@blakeembrey
- [`jshttp/content-type`](https://github.com/jshttp/content-type): @blakeembrey
- [`jshttp/cookie`](https://github.com/jshttp/cookie)：@blakeembrey
- [`jshttp/etag`](https://github.com/jshttp/etag): @blakeembrey
- [`jshttp/forwarded`](https://github.com/jshttp/forwarded): @blakeembrey
- [`jshttp/fresh`](https://github.com/jshttp/fresh): @blakeembrey
- [`jshttp/http-assert`](https://github.com/jshttp/http-assert): @wesleytodd, @jonchurch, @ulisesGascon
- [`jshttp/http-errors`](https://github.com/jshttp/http-errors): @wesleytodd, @jonchurch, @ulisesGascon
- [`jshttp/media-typer`](https://github.com/jshttp/media-typer): @blakeembrey
- [`jshtp/methods`](https://github.com/jshttp/methods)：@blakeembrey
- [`jshttp/mime-db`](https://github.com/jshttp/mime-db): @blakeembrey, @UlisesGascon
- [`jshttp/mime-types`](https://github.com/jshttp/mime-types)：@blakeembrey, @UlisesGascon
- [`jshttp/negotiator`](https://github.com/jshttp/negotiator)：@blakeembrey
- [`jshttp/on-finished`](https://github.com/jshttp/on-finished): @wesleytodd, @ulisesGascon
- [`jshttp/on-headers`](https://github.com/jshttp/on-headers): @blakeembrey
- [`jshttp/proxy-addr`](https://github.com/jshttp/proxy-addr): @wesleytodd, @ulisesGascon
- [`jshttp/range-parser`](https://github.com/jshttp/range-parser): @blakeembrey
- [`jshttp/statuses`](https://github.com/jshttp/statuses): @blakeembrey
- [`jshttp/type-is`](https://github.com/jshttp/type-is): @blakeembrey
- [`jshttp/vary`](https://github.com/jshttp/vary): @blakeembrey
- [`pillarjs/cookies`](https://github.com/pillarjs/cookies)：@blakeembrey
- [`pillarjs/csrf`](https://github.com/pillarjs/csrf): @ulisesGascon
- [`pillarjs/encodeurl`](https://github.com/pillarjs/encodeurl): @blakeembrey
- [`pillarjs/finalhandler`](https://github.com/pillarjs/finalhandler): @wesleytodd, @ulisesGascon
- [`pillarjs/hbs`](https://github.com/pillarjs/hbs)：@ulisesGascon
- [`pillarjs/multiparty`](https://github.com/pillarjs/multiparty)：@blakeembrey
- [`pillarjs/parseurl`](https://github.com/pillarjs/parseurl): @blakeembrey
- [`pillarjs/path-to-regexp`](https://github.com/pillarjs/path-to-regexp): @blakeembrey
- [`pillarjs/request`](https://github.com/pillarjs/request)：@wesleytodd
- [`pillarjs/resolve-path`](https://github.com/pillarjs/resolve-path)：@blakeembrey
- [`pillarjs/router`](https://github.com/pillarjs/router)：@wesleytodd，@ulisesGascon
- [`pillarjs/send`](https://github.com/pillarjs/send)：@blakeembrey
- [`pillarjs/undering-csrf`](https://github.com/pillarjs/understanding-csrf)：@ulisesGascon

#### 目前的倡议Captains

- 试用团队 [ref](https://github.com/expressjs/discussions/issues/227): @UlisesGascon

### 开发者原产地证书 1.1

```text
By making a contribution to this project, I certify that:

 (a) The contribution was created in whole or in part by me and I
     have the right to submit it under the open source license
     indicated in the file; or

 (b) The contribution is based upon previous work that, to the best
     of my knowledge, is covered under an appropriate open source
     license and I have the right under that license to submit that
     work with modifications, whether created in whole or in part
     by me, under the same open source license (unless I am
     permitted to submit under a different license), as indicated
     in the file; or

 (c) The contribution was provided directly to me by some other
     person who certified (a), (b) or (c) and I have not modified
     it.

 (d) I understand and agree that this project and the contribution
     are public and that a record of the contribution (including all
     personal information I submit with it, including my sign-off) is
     maintained indefinitely and may be redistributed consistent with
     this project or the open source license(s) involved.
```

## 协作者指南

<!-- SRC: expressjs/express Collaborator-Guide.md -->

### 网站问题

在 https://github.com/expressjs/expresjs.com中打开的 expresjs.com。

### PR和代码贡献

- 测试必须通过.
- 按照[JavaScript 标准样式](https://standardjs.com/) 和 `npm 运行行`.
- 如果您修复了一个 bug，请添加一个测试。

### 分支

使用 "master" 分支来修复错误或用于当前版本流的
的次要工作。

使用相应名称的分支，例如`5.0`，获取任何用于
未来发布的Express。

### 贡献步骤

1. 为您想要修复的
 bug或您想要添加的功能创建一个问题。
2. Create your own [fork](https://github.com/expressjs/express) on GitHub, then
 checkout your fork.
3. 在您的本地副本中写入您的代码。 为
 创建一个分支是好的做法，你每个新的问题都要处理，但不是强制性的。
4. 若要运行测试套件，首先通过运行 `npm install`，
 先运行 `npm test` 来安装依赖关系。
5. 请确保您的代码通过运行 `npm 运行行` - 修复您
 看到的任何问题。
6. 如果测试通过, 你可以将更改提交给你的叉, 然后从那里创建一个
 拉取请求。 请确保从拉取的
 请求评论中引用您的问题，包括问题号，例如 `#123` 。

### 1) 是问题的问题

我们通常会关闭一些您写入的
应用程序特有的模糊问题或问题。 Please double check the docs and other references before
being trigger happy with posting a question issue.

有助于查看您的问题的事物：

- 完整且可运行的 JS 代码。
- 清除问题或意外行为的描述。
- 对预期结果的清晰描述。
- 你自己已经采取的调试步骤。

如果您提出了一个问题，而不是概述上述项目或使
更容易理解和复制您的问题。 它将被关闭。

## 安全政策和程序

<!-- SRC: expressjs/express Security.md -->

本文档概述了Express
项目的安全程序和一般政策。

- [Reporting a Bug](#reporting-a-bug)
- [Disclosure Policy](#disclosure-policy)
- [关于此政策的评论](#comments-on-this-policy)

### 报告错误

快递团队和社区严肃对待所有安全漏洞。
感谢您改善快乐的安全性。 我们赞赏您的努力和
负责任的披露，并将尽一切努力承认您的
贡献。

发送电子邮件给“express-security@lists.openjsf.org”来报告安全漏洞。

To ensure the timely response to your report, please ensure that the entirety
of the report is contained within the email body and not solely behind a web
link or an attachment.

The lead maintainer will acknowledge your email within 48 hours, and will send a
more detailed response within 48 hours indicating the next steps in handling
your report. 在对您的报告做出初步答复之后。 安全团队将会
努力让您随时了解修复和完整的
通知的进展情况， 并可要求提供补充资料或指导。

将第三方模块中的安全漏洞报告给维护
模块的人或团队。

### 预发布版本

Alpha 和 Beta 的释放不稳定并且\*\*不适合生产使用。
在释放前发现的脆弱性应根据[报告错误](#reporting-a-bug)部分加以报告。
由于该分支的不稳定性，无法保证在下次释放前能够释放任何修复。

### 披露政策

当安全团队收到安全错误报告时，他们会将其分配给一个
主要处理器。 此人将协调修复和释放过程，
涉及以下步骤：

- 确认问题并确定受影响的版本。
- 查找任何潜在的类似问题的审核代码。
- 准备修复所有仍在维护中的释放。 These fixes will be
 released as fast as possible to npm.

### 快递威胁模型

We are currently working on a new version of the security model, the most updated version can be found [here](https://github.com/expressjs/security-wg/blob/main/docs/ThreatModel.md)

### 对此策略的评论

如果您有关于如何改进此进程的建议，请提交一个
拉取请求。

----

# Contributing to Expressjs.com {#expressjs-website-contributing}

<!-- LOCAL: expressjs/expressjs.com ../../CONTRIBUTING.md -->

### Express JS 框架的官方文档

这是 [Expressjs.com](https://github.com/expressjs/expressjs.com)网站的贡献文档。

#### 需要一些想法吗？ 这些是一些典型的问题。

1. **网站问题**:
 如果您看到网站上任何可以使用调整的东西，请考虑如何修复它。

 - 显示或屏幕大小问题
 - 流动响应问题
 - 缺少或损坏的辅助功能
 - 网站中止
 - 断开链接
 - 页面结构或用户界面改进

2. **内容问题**：
 修复任何与网站内容或打包相关的内容。
 - 拼写错误
 - 不正确/过时的快递JS 文档
 - 缺少内容

3. **翻译问题**：修复翻译错误或贡献新内容。
 - 修复拼写错误
 - 修复不正确/翻译不良的单词
 - 翻译新内容

> **IMPORTANT：**
> 所有翻译提交目前已暂停。 更多信息请参阅此 [notice](#notice-we-have-paused-all-translation-contributions)。

- 查看下面的[贡献翻译](#contributing-translations)部分以获取贡献指南。

#### 想要处理积压问题？

我们常常有需要工作的缺陷或改进。 您可以在我们的仓库中找到这些[Issues tab](https://github.com/expressjs/expressjs.com/issues)。 看看标签来找到与您相匹配的东西。

#### 有想法吗？ 发现错误？

如果您发现了一个错误或轮胎，或者如果您有一个增强功能的想法，您可以：

- 在我们的仓库上提交一个[新问题](https://github.com/expressjs/expressjs.com/issues/new/choose)。 对较大的建议执行此操作，或者如果您想先讨论或获得反馈。
- Make a [Github pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request). 如果你已经完成了工作并且已经准备就绪，请随时发送。

## 入门

下面的步骤将指导您通过 Expressjs.com 贡献过程。

#### 第 1 步：(OPTIONAL) 打开一个新问题

所以你发现了一个你想要解决的问题，或者有一个你想要解决的网站升级问题。

1. 如果您想要得到反馈或讨论，请在开始工作前打开讨论 [issue](https://github.com/expressjs/expressjs.com/issues/new/choose)。 这并不是需要的，而是鼓励提出更大的建议。
 - 虽然我们非常鼓励采取这一步骤，但这只是对提出重大修改意见的材料而言。 它有助于我们澄清和突出工作重点，并确保它与总体项目优先事项保持一致。
 - 对于提议稍作改进或更正的呈件，不需要这样做。 你可以跳过这一步。
 - 当开始一个问题时，请给它一个标题并填写描述部分。 您提供的详细信息越多，我们可以提供的反馈就越多。

2. 收到您的问题后，快递JS 文档团队将提供反馈。 我们阅读了每一份呈件，并且总是试图以反馈方式迅速作出反应。
 - 对于提议作出重大修改的呈件，我们鼓励你在开始工作之前遵循审查进程。

#### 第 2 步：获取应用程序代码库

复制仓库并获取代码：

```
git clone https://github.com/expressjs/expressjs.com.git
```

在你有了代码后，你准备好开始做出更改！

但只是在你需要另外一点解释的情况下， 以下各节概述了代码库的主要章节，其中可能会作大部分修改。

**Markdown 页面文件**:

- 这些文件渲染为 html 并构成站点的单个页面。 网站的大部分文档文本内容都写入了 `md` 文件。
- 更改这些更改以更改个别页面的内容/文本或标记。
- 每种语文都有自己的一整套网页， 位于他们各自的语言目录下——所有西班牙的Markdown 内容都可以在 `es` 目录中找到。

**包括部分和布局模板**

- `_includes` 是多页导入并重新使用的partials。
 - 这些被用来导入文本内容，供各页重复使用，例如API文档。 ，`_include > api > en > 5x`，包含在每种语言中。
 - 这些是用来包括构成全站用户界面和外围结构的页面组件，如头、页脚等。
- `_layouts` 是用来包装站点个别页面的模板。
 - 这些用于显示站点外围结构，如页眉和页脚。 并且在 `content` 标签内注入和显示单个Markdown页面。

**博客Markdown 文件**

- 这些文件构成单独的博客帖子。 If you want to contribute a blog post please
 follow the specific instructions for [How to write a blog post.](https://expressjs.com/en/blog/write-post.html)
- 位于`_posts`目录下。

**CSS or Javascript**

- 所有css和js文件都保存在项目根目录下的`css`和`js`文件夹中。

Express JS 网站正在使用 [Jeykyll](https://jekyllrb.com/)构建，并位于[Github Pages](https://pages.github.com/)。

#### 第 3 步：运行应用程序

现在你需要看到你的更改，这意味着你需要一个运行中的应用程序版本。 您有两个选项。

1. **Run Locally**：这将使应用程序的本地版本在您的机器上运行。 按照我们的 [本地设置指南] (https://github.com/expressjs/expressjs.com?tab=readme-ov-file#local-setup) 使用此选项。
 - 这是适度到复杂的工作的推荐选择。
2. **Run 使用 Deplost Preview**: 如果您不想在本地安装时使用此选项。 我们连续集成管道的一部分包括 [Netlify Deplavily Preview](https://docs.netlify.com/site-deploys/deploy-previews/)。
 1. 要使用这个功能，您需要在线获取您的更改——在您对功能分支做出首次承诺后， 做一个_草稿_拉取请求。
 2. 构建步骤完成后，您将能够访问 __Deplusing Preview_选项卡，该选项卡将在网络上运行您的更改， 每次承诺后的重建都被推进。
 3. 当你完全完成你的工作并准备好审查后，删除你的合并请求上的草稿状态并提交你的工作。

## 贡献翻译

#### 注意：我们已暂停所有翻译贡献。

> **IMPORTANT：**
> 我们正在努力实现更简化的翻译工作流程。 只要发布此通知，我们将不接受任何翻译提交。

我们非常鼓励社区翻译！ 我们不再有专业翻译，我们相信我们社区能够提供准确和有益的翻译。

文件被翻译成这些语言：

- 英文（`en`）
- 西班牙语(`es`)
- 法语(“fr”)
- 意大利文(`it`)
- 印度尼西亚语(id\`)
- 日语 (`ja`)
- 韩语 (`ko`)
- 巴西葡萄牙语(“pt-br”)
- 俄语(`ru`)
- Slovak (`sk`)
- 泰语(`th`)
- 土耳其语(“tr”)
- 乌克兰语(“uk”)
- Uzbek (`uz`)
- 简体中文 (zh-cn\`)
- 繁体中文 (zh-tw\`)

### 添加全站翻译中

如果您在列表中找不到翻译，您可以创建一个新的翻译。

要将 Expressjs.com 翻译成新的语言，请遵循以下步骤：

1. Clone the [`expressjs.com`](https://github.com/expressjs/expressjs.com) repository.
2. 使用[ISO 639-1代码](https://www.loc.gov/standards/iso639-2/php/code_list.php)创建您选择的语言目录作为其名称。
3. 复制`index.md`, `api.md`, `starter/`, `guide/`, `advanced/`, `resources/`, `4x/`, 和 `3x/`, 到语言目录。
4. 从“API Reference”菜单中删除到 2.x 文档的链接。
5. 更新复制的Markdown文件中的`lang`变量。
6. 更新复制的Markdown文件中的`title`变量。
7. 为`_includes/`目录中的语言创建页眉、页脚、通知和通知文件 在各自的目录中，并对目录进行必要的编辑。
8. 在`_includes/`目录中为语言创建公告文件。
9. Make sure to append `/{{ page.lang }}` to all the links within the site.
10. 使用新语言更新 [CONTRIBUTING.md](https://github.com/expressjs/expressjs.com/blob/gh-pages/CONTRIBUTING.md#contributing-translations) 和 `.github/workflows/translation.yml` 文件。

### 添加页面和部分翻译

许多网站翻译仍然缺少页面。 要找到我们需要帮助的人，您可以[过滤合并的 PRs](https://github.com/expressjs/expressjs.com/pulls?q=is%3Apr+is%3Aclosed+label%3Arequires-translation-es) 包含您的语言标签。 例如`requires-translation-es`需要西班牙语翻译。

如果您贡献了一个页面或部分翻译，请参考原始PR。 这有助于合并您的翻译，从原始的 PR中移除标签。
