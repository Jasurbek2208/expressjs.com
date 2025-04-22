---
layout: page
title: Expressに貢献する
description: Express.jsに貢献する方法については、問題の報告、プルリクエストの提出、協力者となること、セキュリティポリシーの理解などをご覧ください。
menu: resources
lang: en
redirect_from: ""
---

# Expressに貢献する

### Expressjs.comに貢献したいですか？ Click [here](#expressjs-website-contributing).

Express and the other projects in the [expressjs organization on GitHub](https://github.com/expressjs) are projects of the [OpenJs Foundation](https://openjsf.org/).
これらのプロジェクトは、Node.js財団の一般的なポリシーとガイドライン、および以下の追加のガイドラインに準拠しています。

- [Technical committee](#technical-committee)
- [Community contributing guide](#community-contributing-guide)
- [Collaborator's guide](#collaborators-guide)
- [Security policies and procedures](#security-policies-and-procedures)

## 技術委員会

Express技術委員会は、アクティブなプロジェクトメンバーで構成され、Expressプロジェクトの開発とメンテナンスをガイドします。 詳細については、[Express Community - Technical Committee](community.html#technical-committee)を参照してください。

## コミュニティ貢献ガイド

<!-- SRC: expressjs/express Contributing.md -->

このドキュメントの目標は、以下のような貢献プロセスを作成することです。

- 新しい貢献を奨励します。
- 貢献者が関与し続けるよう促す。
- 不必要なプロセスや官僚機構を可能な限り避けます。
- 貢献者がどのように意思決定に関わることができるかを明確にする透明な意思決定プロセスを作成します。

### ボキャブラリー

- **コントリビューター** は課題やプルリクエストに対するコメントや作成を行う個人です。
- **Committer** は、リポジトリへの書き込みアクセス権を与えられた貢献者のサブセットです。
- **Project Captain** はリポジトリのリードメンテナーです。
- \*\*TC (Technical Committee)\*\*は希少な紛争を解決するために必要な技術
 の専門知識を代表するコミッターグループです。
- **Triager** は、リポジトリへのトリアージアクセスを与えられた貢献者のサブセットです。

### ログの問題

質問または問題の問題を記録します。 When in doubt, log an issue, and
any additional policies about what to include will be provided in the responses. 唯一
例外は、私的に送信されるべきセキュリティディスクロージャーです。

コミッターはあなたを別のリポジトリに誘導し、追加の説明を求め、問題が解決される前に
適切なメタデータを追加することができます。

礼儀正しく、尊敬してください。 すべての参加者は、
プロジェクトの行動規範に従うことが期待されます。

### 貢献

このリポジトリのリソースへの変更は、プルリクエストでなければなりません。 これは、ドキュメント、コード、バイナリファイルなどのすべての変更
に適用されます。 長期的なコミッターやTCメンバーであっても、
プルリクエストを使用する必要があります。

レビューされずにプルリクエストをマージすることはできません。

些細な貢献ではない場合、他のタイムゾーンの
貢献者がレビューする時間があることを確認するために、プルリクエストは少なくとも36時間座る必要があります。
の週末やその他の休暇期間にも配慮しなければならず、アクティブなコミッターが
議論とレビューのプロセスに参加するまでの合理的な時間を確保することができます。

各コントリビューションのデフォルトは、コミッターが異議を持たない場合に受け入れられることです。
During a review, committers may also request that a specific contributor who is most versed in a
particular area gives a "LGTM" before the PR can be merged. 土地への貢献のための追加の「サインオフ」
プロセスはありません。 Once all issues brought by committers are addressed it can
be landed by any committer.

別のコミッターによってプルリクエストで異議が提起された場合。
コミッターは、議論によって
表明される懸念に対処する方法により、コンセンサスに到達しようとすべきです。 提案された変更の妥協、または変更の撤回。

もし貢献が論争の的であり、コミッターが
の着陸方法について同意できない場合、または着陸すべき場合は、TCにエスカレートさせる必要があります。 TCメンバーは、決議を見つけるために、保留中の貢献について定期的に
議論すべきです。 解決のためにTCには
少数の問題しか持ち込まれず、その議論とコミッター間の
妥協がデフォルトの解決メカニズムであることが期待されます。

### Triager になる

誰でもトリアージになれます！
[triage process document](https://github.com/expressjs/express/blob/master/Triager-Guide.md)でトリガーになるプロセスの詳細をお読みください。

Currently, any existing [organization member](https://github.com/orgs/expressjs/people) can nominate
a new triager. トリアガーになることに興味があるなら 私たちの最善のアドバイスは、トリアージやプルリクエストを支援することによって、コミュニティで
積極的に参加することです。 また、
は、TC会議に参加したり、Slack
の議論に参加したりするなど、他のコミュニティ活動に参加することをお勧めします。 If you feel ready and have been helping triage some issues, reach out to an active member of the organization to ask if they'd
be willing to support you. 同意すれば、指名を正式化するプルリクエストを作成できます。 指名に異議を申し立てた場合、トリアージチームは関与する個人と協力し、解決策を見つける責任があります。

You can also reach out to any of the [organization members](https://github.com/orgs/expressjs/people)
if you have questions or need guidance.

### コミッターになる

重要かつ貴重な貢献をしたすべての貢献者は、適時にオンボーディングする必要があります。
とコミッターとして追加され、リポジトリへの書き込みアクセス権が与えられます。

コミッターはこのポリシーに従い、引き続きプルリクエストを送信することが期待されています。
適切なレビューを行い、他のコミッターにプルリクエストをマージさせます。

### TC プロセス

TCは、TCにエスカレートされた問題について「コンセンサスを求める」プロセスを使用します。
グループは、TCメンバーの間に開かれた異議を持たない決議を見つけようとします。
異議がないコンセンサスに到達できない場合は、多数決が
と呼ばれます。 また、TCによって行われた決定の大部分が
合意形成プロセスを通じて行われ、投票は最後の手段としてのみ使用されることが期待されます。

解決には、
合意に向けて前進する方法についての提案をプロジェクトキャプテンにこの問題を返すことが含まれます。 TCの
会議では、その会議中に議題に関するすべての問題が解決されることは期待されておらず、プロジェクトキャプテン間で起こっている議論を
継続することを好むかもしれません。

メンバーはいつでもTCに追加できます。 Any TC member can nominate another committer
to the TC and the TC uses its standard consensus seeking process to evaluate whether or
not to add this new member. TCは、最低3人のアクティブメンバーと最大10の
で構成されます。 TCが5人未満の場合、アクティブなTCメンバーは
新しい誰かを指名する必要があります。 TCメンバーが辞任している場合、彼らは
誰かに代わってもらうように指名することを奨励されます(必須ではありません)。

TCメンバーは、役割で有効であるために必要な
としてGithub組織、npm組織、およびその他のリソースに管理者として追加されます。

TCメンバーが過去12ヶ月以内に参加し、
連続したTCミーティングを見逃す必要があります。 Our goal is to increase participation, not punish
people for any lack of participation, this guideline should be only be used as such
(replace an inactive member with a new active one, for example). この
を満たしていないメンバーは辞退することが求められます。 TCメンバーがステップダウンしない場合、
ディスカッションリポジトリで問題を開き、それらを非アクティブ状態に移動できます。
により停止または削除されたTCメンバーは、非アクティブ状態に移動されます。

Inactive status members can become active members by self nomination if the TC is not already
larger than the maximum of 10. 最大サイズで、
アクティブなメンバーが下にステップダウンした場合、彼らはまた好みを与えられます。

### プロジェクトキャプテンズ

Express TC では、
組織内の個々のプロジェクト/リポジトリのキャプテンを指定できます。 これらのキャプテンは、技術的およびコミュニティの前線でレポの主要な
日々のメンテナーであることに責任があります。
リポジトリのキャプテンは、リポジトリの所有権とパッケージの公開権を与えられます。
When there are conflicts, especially on topics that effect the Express project
at large, captains are responsible to raise it up to the TC and drive
those conflicts to resolution. Captains are also responsible for making sure
community members follow the community guidelines, maintaining the repo
and the published package, as well as in providing user support.

TCメンバーと同じように、レポキャプテンはコミッターの一部です。

プロジェクトのキャプテンになるためには、候補者はリクエストの前に少なくとも6ヶ月間その
プロジェクトに参加することが期待されます。
がコードの貢献とトリアージの問題を助けてくれるはずです。 また、
がGitHubとNPMの両方のアカウントで2FAを有効にしている必要があります。

**同じ**リポジトリのTCメンバーまたは既存のキャプテンは、キャプテン役に別のコミッター
を指名することができます。 そのためには、この文書にPRを提出する必要があります。
**アクティブなプロジェクトキャプテン** セクション (並び替え順を維持しながら) をプロジェクト
名で更新します。 ノミネート者のGitHubハンドルとそのnpmユーザー名 (異なる場合)。

- レポは、仕事の範囲にとって意味のあるできるだけ多くのキャプテンを持つことができます。
- TCメンバーまたは既存のリポジトリキャプテンは**同じプロジェクトにあります**。新しいキャプテンを指名できます。
 他のプロジェクトからのレポキャプテンは、別のプロジェクトにキャプテンを指名してはいけません。

PRは、TCメンバーから少なくとも2件の承認が必要であり、コメントおよび/または反対のために
を許可する2週間の保留期間が必要です。  PRがマージされると、TCメンバーはそれを
適切なGitHub/npmグループに追加します。

#### アクティブなプロジェクトとキャプテンズ

- [`expressjs/badgeboard`](https://github.com/expressjs/badgeboard): @wesleytodd
- [`express/basic-auth-connect`](https://github.com/expressjs/basic-auth-connect): @ulisesGascon
- [`expressjs/body-parser`](https://github.com/expressjs/body-parser): @wesleytodd, @jonchurch, @ulisesGascon
- [`express/compression`](https://github.com/expressjs/compression): @ulisesGascon
- [`expressjs/connect-multiparty`](https://github.com/expressjs/connect-multiparty): @ulisesGascon
- [`expressjs/cookie-parser`](https://github.com/expressjs/cookie-parser): @wesleytodd, @UlisesGascon
- [`expressjs/cookie-session`](https://github.com/expressjs/cookie-session): @ulisesGascon
- [`expressjs/cors`](https://github.com/expressjs/cors): @jonchurch, @ulisesGascon
- [`express/discussions`](https://github.com/expressjs/discussions): @wesleytodd
- [`expressjs/errorhandler`](https://github.com/expressjs/errorhandler): @ulisesGascon
- [`express/express-paginate`](https://github.com/expressjs/express-paginate): @ulisesGascon
- [`expressjs/express`](https://github.com/expressjs/express): @wesleytodd, @ulisesGascon
- [`express/expressjs.com`](https://github.com/expressjs/expressjs.com): @crandmck, @jonchurch, @bjohansebas
- [`expressjs/flash`](https://github.com/expressjs/flash): @ulisesGascon
- [`expressjs/generator`](https://github.com/expressjs/generator): @wesleytodd
- [`expressjs/method-override`](https://github.com/expressjs/method-override): @ulisesGascon
- [`expressjs/morgan`](https://github.com/expressjs/morgan): @jonchurch, @ulisesGascon
- [`expressjs/multer`](https://github.com/expressjs/multer): @LinusU, @ulisesGascon
- [`expressjs/response-time`](https://github.com/expressjs/response-time): @UlisesGascon
- [`expressjs/serve-favicon`](https://github.com/expressjs/serve-favicon): @ulisesGascon
- [`express/serve-index`](https://github.com/expressjs/serve-index): @ulisesGascon
- [`express/serve-static`](https://github.com/expressjs/serve-static): @ulisesGascon
- [`expressjs/session`](https://github.com/expressjs/session): @ulisesGascon
- [`expressjs/statusboard`](https://github.com/expressjs/statusboard): @wesleytodd
- [`expressjs/timeout`](https://github.com/expressjs/timeout): @ulisesGascon
- [`expressjs/vhost`](https://github.com/expressjs/vhost): @ulisesGascon
- [`jshttp/accepts`](https://github.com/jshttp/accepts): @blakeembrey
- [`jshttp/basic-auth`](https://github.com/jshttp/basic-auth): @blakeembrey
- [`jshttp/compressible`](https://github.com/jshttp/compressible): @blakeembrey
- [`jshttp/content-disposition`](https://github.com/jshttp/content-disposition): @blakeembrey
- [`jshttp/content-type`](https://github.com/jshttp/content-type): @blakeembrey
- [`jshttp/cookie`](https://github.com/jshttp/cookie): @blakeembrey
- [`jshttp/etag`](https://github.com/jshttp/etag): @blakeembrey
- [`jshttp/forwarded`](https://github.com/jshttp/forwarded): @blakeembrey
- [`jshttp/fresh`](https://github.com/jshttp/fresh): @blakeembrey
- [`jshttp/http-assert`](https://github.com/jshttp/http-assert): @wesleytodd, @jonchurch, @ulisesGascon
- [`jshttp/http-errors`](https://github.com/jshttp/http-errors): @wesleytodd, @jonchurch, @ulisesGascon
- [`jshttp/media-typer`](https://github.com/jshttp/media-typer): @blakeembrey
- [`jshttp/methods`](https://github.com/jshttp/methods): @blakeembrey
- [`jshttp/mime-db`](https://github.com/jshttp/mime-db): @blakeembrey, @UlisesGascon
- [`jshttp/mime-types`](https://github.com/jshttp/mime-types): @blakeembrey, @UlisesGascon
- [`jshttp/negotiator`](https://github.com/jshttp/negotiator): @blakeembrey
- [`jshttp/on-finished`](https://github.com/jshttp/on-finished): @wesleytodd, @ulisesGasson
- [`jshttp/on-headers`](https://github.com/jshttp/on-headers): @blakeembrey
- [`jshttp/proxy-addr`](https://github.com/jshttp/proxy-addr): @wesleytodd, @ulisesGascon
- [`jshttp/range-parser`](https://github.com/jshttp/range-parser): @blakeembrey
- [`jshttp/statuses`](https://github.com/jshttp/statuses): @blakeembrey
- [`jshttp/type-is`](https://github.com/jshttp/type-is): @blakeembrey
- [`jshttp/vary`](https://github.com/jshttp/vary): @blakeembrey
- [`pillarjs/cookies`](https://github.com/pillarjs/cookies): @blakeembrey
- [`pillarjs/csrf`](https://github.com/pillarjs/csrf): @ulisesGascon
- [`pillarjs/encodeurl`](https://github.com/pillarjs/encodeurl): @blakeembrey
- [`pillarjs/finalhandler`](https://github.com/pillarjs/finalhandler): @wesleytodd, @ulisesGascon
- [`pillarjs/hbs`](https://github.com/pillarjs/hbs): @ulisesGascon
- [`pillarjs/multiparty`](https://github.com/pillarjs/multiparty): @blakeembrey
- [`pillarjs/parseurl`](https://github.com/pillarjs/parseurl): @blakeembrey
- [`pillarjs/path-to-regexp`](https://github.com/pillarjs/path-to-regexp): @blakeembrey
- [`pillarjs/request`](https://github.com/pillarjs/request): @wesleytodd
- [`pillarjs/resolve-path`](https://github.com/pillarjs/resolve-path): @blakeembrey
- [`pillarjs/router`](https://github.com/pillarjs/router): @wesleytodd, @ulisesGascon
- [`pillarjs/send`](https://github.com/pillarjs/send): @blakeembrey
- [`pillarjs/understanding-csrf`](https://github.com/pillarjs/understanding-csrf): @ulisesGascon

#### 現在のイニシアチブのキャプテン数

- トリアージチーム [ref](https://github.com/expressjs/discussions/issues/227): @UlisesGascon

### 開発者証明書発行元 1.1

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

## コラボレーターのガイド

<!-- SRC: expressjs/express Collaborator-Guide.md -->

### ウェブサイトの問題

expressjs.com ウェブサイトの https://github.com/expressjs/expressjs.com で問題を開きます。

### PRとコードの貢献

- テストは合格しなければなりません。
- [JavaScript Standard Style](https://standardjs.com/) と `npm run lint` をフォローします。
- バグを修正する場合は、テストを追加します。

### ブランチ

`master` ブランチを使用して、現在のリリースストリームの
を意図したバグ修正やマイナーな作業を行ってください。

Expressの将来のリリースである
を想定したものには、`5.0`のような名前付きブランチを使用してください。

### 貢献するためのステップ

1. [Create an issue](https://github.com/expressjs/express/issues/new) for the
 bug you want to fix or the feature that you want to add.
2. Create your own [fork](https://github.com/expressjs/express) on GitHub, then
 checkout your fork.
3. ローカルコピーにコードを書きなさい。 必須ではありませんが、新しい課題ごとに
 ブランチを作成することは良い方法です。
4. テストスイートを実行するには、`npm install`、
 を実行し、`npm test`を実行して依存関係をインストールします。
5. Ensure your code is linted by running `npm run lint` -- fix any issue you
 see listed.
6. テストが合格した場合、変更をフォークに反映し、そこから
 プルリクエストを作成することができます。 Issue 番号を含めることで、プル
 リクエストのコメントを参照してください。例：`#123`。

### 質問である問題

私たちは通常、あなたが書いているいくつかの
アプリに固有の漠然とした問題や質問を閉じます。 Please double check the docs and other references before
being trigger happy with posting a question issue.

あなたの質問の問題を確認するのに役立つことは次のとおりです。

- 完全かつ実行可能なJSコード。
- 問題の説明または予期しない動作をクリアします。
- 期待される結果の明確な説明。
- あなた自身でデバッグするために取ったステップ。

質問を投稿し、上記の項目を概説したり、
問題を理解し、再現することが容易になる場合。 閉店します

## セキュリティポリシーと手順

<!-- SRC: expressjs/express Security.md -->

このドキュメントでは、Express
プロジェクトのセキュリティ手順と一般的なポリシーについて概説しています。

- [Reporting a Bug](#reporting-a-bug)
- [Disclosure Policy](#disclosure-policy)
- [Comments on this Policy](#comments-on-this-policy)

### バグの報告

Express チームとコミュニティは、Express のすべてのセキュリティ上のバグを真剣に受け止めています。
Express のセキュリティを向上させていただきありがとうございます。 私たちはあなたの努力と
責任ある開示に感謝し、あなたの
貢献を認めるためにあらゆる努力をします。

`express-security@lists.openjsf.org` にメールしてセキュリティバグを報告してください。

レポートへの適時の対応を確保するために。 レポートの
全体が電子メール本文内に含まれていることを確認してください。また、Webの
リンクまたは添付のみに含まれていないことを確認してください。

The lead maintainer will acknowledge your email within 48 hours, and will send a
more detailed response within 48 hours indicating the next steps in handling
your report. レポートへの最初の返信後 セキュリティチームは、
修正と完全な
発表に向けた進捗状況をお知らせするよう努めます。 追加情報やガイダンスを求めることもあります

Report security bugs in third-party modules to the person or team maintaining
the module.

### プレリリースバージョン

アルファ版とベータ版のリリースは不安定で、**本番用には適していません**。
Vulnerabilities found in pre-releases should be reported according to the [Reporting a Bug](#reporting-a-bug) section.
ブランチの不安定な性質のため、次回のプレリリースでは修正がリリースされることは保証されません。

### 開示方針

セキュリティチームがセキュリティバグレポートを受け取ると、セキュリティバグレポートは
プライマリハンドラに割り当てられます。 This person will coordinate the fix and release process,
involving the following steps:

- 問題を確認し、影響を受けるバージョンを確認します。
- 潜在的な同様の問題を見つけるために監査コード。
- メンテナンス中のすべてのリリースの修正を準備します。 これらの修正は、npmにできるだけ早く
 リリースされます。

### Express 脅威モデル

現在、セキュリティモデルの新しいバージョンに取り組んでいます。最新のバージョンは [here](https://github.com/expressjs/security-wg/blob/main/docs/ThreatModel.md) を見つけることができます。

### 本ポリシーに関するコメント

このプロセスがどのように改善されるかについての提案がある場合は、
プルリクエストを送信してください。

----

# Expressjs.com {#expressjs-website-contributing} への貢献

<!-- LOCAL: expressjs/expressjs.com ../../CONTRIBUTING.md -->

### Express JS Frameworkの公式ドキュメント

これは [Expressjs.com](https://github.com/expressjs/expressjs.com) ウェブサイトのコントリビューションドキュメントです。

#### アイデアが必要ですか？ これらは典型的な問題です

1. **ウェブサイトの問題**:
 チューンアップを使用できるサイトで何かが見つかった場合は、それをどのように修正するかを考えてください。

 - ディスプレイまたは画面サイズの問題
 - モバイル応答性の問題
 - アクセシビリティ機能が欠けているか壊れています
 - ウェブサイトの停止状況
 - リンクが壊れています
 - ページ構造またはユーザインターフェースの強化

2. **コンテンツの問題**:
 サイトのコンテンツやタイプミスに関する問題を修正しました。
 - スペルエラー
 - ExpressJSのドキュメントを正しくない/古いものにする
 - コンテンツがありません

3. **翻訳の問題**: 翻訳エラーを修正したり、新しいコンテンツを提供したりします。
 - スペルミスの修正
 - 間違った/不十分な単語を修正する
 - 新しいコンテンツを翻訳

> **重要：**
> すべての翻訳提出物は現在一時停止しています。 詳細については、この [notice](#notice-we-have-paused-all-translation-contributions) を参照してください。

- Check out the [Contributing translations](#contributing-translations) section below for a contributing guide.

#### バックログの問題に取り組んでみたいですか?

多くの場合、作業が必要なバグや機能強化があります。 You can find these under our repo's [Issues tab](https://github.com/expressjs/expressjs.com/issues). タグをチェックして、あなたに合ったものを見つけてください。

#### アイデアがありますか？ バグを見つけましたか？

バグやタイプミスを見つけた場合、または機能強化のアイデアがある場合は、次のことができます。

- Submit a [new issue](https://github.com/expressjs/expressjs.com/issues/new/choose) on our repo. 大規模な提案のためにこれを行う、または最初に議論またはフィードバックを得たい場合。
- Make a [Github pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request). あなたがすでに仕事をしていて、それが行く準備ができている場合は、私たちの方法を送って自由に感じてください。

## 概説

以下の手順でExpressjs.comのコントリビューションプロセスをご案内します。

#### ステップ 1: (任意) 新しい問題を開く

だから、あなたが修正したい、またはあなたが作りたいサイトの機能強化を持っている問題を発見しました。

1. フィードバックやディスカッションを受け取りたい場合は、仕事を始める前にディスカッション [issue](https://github.com/expressjs/expressjs.com/issues/new/choose) を開いてください。 これは必要ではありませんが、より大きな提案のために奨励されます。
 - 私たちはこのステップを強く奨励しますが、それは重要な変更を提案する提出物のためのものです。 作業を明確にし、集中させ、プロジェクト全体の優先順位に合わせるのに役立ちます。
 - 小規模な改善または修正を提案する提出物には、これは必要ありません。 この手順をスキップできます。
 - 課題を開く際にはタイトルを付け、説明欄に記入してください。 あなたが提供する詳細は、より多くのフィードバックを与えることができます。

2. 問題を受け取った後、Express JS のドキュメンテーションチームはフィードバックを送ります。 私たちはすべての提出物を読んで、常にフィードバックで迅速に対応しようとしています。
 - 大幅な変更を提案する提出物については、作業を開始する前にレビュープロセスに従うことをお勧めします。

#### ステップ 2: アプリケーションコードベースを取得

リポジトリをクローンしてコードを取得します。

```
git clone https://github.com/expressjs/expressjs.com.git
```

コードを手に入れたら、変更を始める準備ができます！

しかし、あなたが少し余分な説明が必要な場合に備えて。 このセクションではコードベースのメインセクションの概要を示しています。ほとんどの変更が行われる可能性があります。

**Markdown ページファイル**:

- これらのファイルはhtmlにレンダリングされ、サイトの個々のページを構成します。 サイトのドキュメントテキストコンテンツのほとんどは、`md`ファイルで書かれています。
- これらを変更して、個々のページのコンテンツ/テキストまたはマークアップに変更します。
- 各言語にはそれぞれのページがあります。 それぞれの言語ディレクトリの下にあります。例えば、スペイン語のマークダウンの内容は`es`ディレクトリにあります。

**部分テンプレートとレイアウトテンプレートを含む**

- `_includes` は複数のページでインポートされ再利用される部分です。
 - これらは、API ドキュメントなどのページ間で再利用するためのテキストコンテンツをインポートするために使用されます。 ., `_includes > api > en > 5x`, これはすべての言語に含まれています.
 - これらは、サイト全体のユーザーインターフェイスを構成するページコンポーネントや、ヘッダー、フッターなどの周辺構造を含むために使用されます。
- `_layouts` はサイトの個々のページをラップするために使用されるテンプレートです。
 - これらは、ヘッダーやフッターなどのサイト周辺の構造を表示するために使用されます。 そして `content` タグの中に個々のマークダウンページを挿入したり表示したりするためのものです。

**ブログMarkdown ファイル**

- これらのファイルは、個々のブログ記事を構成します。 If you want to contribute a blog post please
 follow the specific instructions for [How to write a blog post.](https://expressjs.com/en/blog/write-post.html)
- `_posts`ディレクトリの下にあります。

**CSS or Javascript**

- すべての css と js ファイルは、プロジェクトの root 上の `css` と `js` フォルダに保存されます。

Express JS のウェブサイトは [Jeykyll](https://jekyllrb.com/) を使用してビルドされており、[Github Pages](https://pages.github.com/)でホストされています。

#### ステップ 3: アプリケーションの実行

変更を確認する方法が必要になります。つまり、アプリケーションの実行中バージョンが必要になります。 2つの選択肢があります。

1. **Locally**: ローカルバージョンのアプリケーションをマシン上で起動します。 Follow our [Local Setup Guide](https://github.com/expressjs/expressjs.com?tab=readme-ov-file#local-setup) to use this option.
 - これは、中程度から複雑な作業に推奨されるオプションです。
2. **Run using Deploy Preview**: ローカルインストールを気にしたくない場合は、このオプションを使用します。 継続的なインテグレーションパイプラインには、[Netlify Deploy Preview](https://docs.netlify.com/site-deploys/deploy-previews/)が含まれています。
 1. これを使用するには、オンラインで変更を取得する必要があります - フィーチャーブランチで最初にコミットした後。 _ドラフト_ プルリクエストを作成します。
 2. ビルドステップが完了すると、ウェブ上で変更を実行する **Deploy Preview** タブにアクセスできます。 それぞれのコミットが押された後に再構築されます
 3. 作業が完全に完了し、レビューの準備が整ったら、プルリクエストのドラフトステータスを削除し、作業を送信します。

## 翻訳の貢献

#### お知らせ: すべての翻訳投稿を一時停止しました。

> **重要：**
> 現在、より合理的な翻訳ワークフローに向けて取り組んでいます。 この通知が掲載されている限り、翻訳の提出を受け付けません。

コミュニティの翻訳を強くお勧めします！ 私たちはもはやプロの翻訳はありませんし、正確で有益な翻訳を提供するためにコミュニティの力を信じています。

ドキュメントは以下の言語に翻訳されています。

- 英語 (`en`)
- スペイン語 (`es`)
- フランス語 (`fr`)
- Italian (`it`)
- インドネシア語 (`id`)
- 日本語 (`ja`)
- 韓国語（`ko`）
- ブラジルポルトガル語 (`pt-br`)
- ロシア (`ru`)
- Slovak (`sk`)
- タイ (`th`)
- トルコ語 (`tr`)
- ウクライナ語 (`uk`)
- Uzbek (`uz`)
- 簡体字中国語 (`zh-cn`)
- 繁体字中国語 (`zh-tw`)

### 新しいフルサイト翻訳の追加

リストから翻訳が見つからない場合は、新しい翻訳を作成できます。

Expressjs.comを新しい言語に翻訳するには、以下の手順に従ってください。

1. [`expressjs.com`](https://github.com/expressjs/expressjs.com) リポジトリをクローンします。
2. [ISO 639-1 code](https://www.loc.gov/standards/iso639-2/php/code_list.php) を名前として使用して、選択した言語のディレクトリを作成します。
3. `index.md` 、 `api.md` 、 `starter/`、 `guide/`、 `advanced/`、 `resources/`、 `4x/`、 そして `3x/`を言語ディレクトリにコピーします。
4. "API Reference" メニューから 2.x ドキュメントへのリンクを削除します。
5. コピーしたマークダウンファイルの `lang` 変数を更新します。
6. コピーしたマークダウンファイル内の変数`title`を更新します。
7. `_includes/`ディレクトリにある言語のヘッダー、フッター、通知、お知らせファイルを作成します。 内容を編集する必要があります
8. `_includes/`ディレクトリに言語のアナウンスファイルを作成します。
9. サイト内のすべてのリンクに `/{{ page.lang }}` を追加してください。
10. [CONTRIBUTING.md](https://github.com/expressjs/expressjs.com/blob/gh-pages/CONTRIBUTING.md#contributing-translations) と `.github/workflows/translation.yml` ファイルを新しい言語で更新します。

### ページとセクションの翻訳を追加する

多くのサイト翻訳はまだページがありません。 ヘルプが必要なものを見つけるには、あなたの言語のタグを含む [filter for merged PRs](https://github.com/expressjs/expressjs.com/pulls?q=is%3Apr+is%3Aclosed+label%3Arequires-translation-es) を使用します。 例えば、 `requires-translation-es` はスペイン語の翻訳が必要です。

ページやセクションの翻訳を行う場合は、オリジナルのPRを参照してください。 これにより、翻訳をマージして元のPRからタグを削除することができます。
