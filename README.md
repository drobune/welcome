![](https://www.iro-d-ori.co.jp/img/og.png)

# irodori How-To-Work

この資料はイロドリ社での仕事に対する考え方や作業方法をまとめています。

## はじめに
こんにちは！devkatoです。

あなたがこの資料を見ているということは、何らかの関係でイロドリ社の仕事に関わっているということですね？

まずはこれからよろしくお願いします！一緒によい仕事をしましょう！


## 僕達が大事にしているもの

### ■ パフォーマンス
関わり方はどうであれ、自分が **一番パフォーマンスを出せるための環境** を自分で見つける/作ることを心がけてください。

必要な書籍/機材等、会社でサポートできるものについては可能な限り揃えます。

### ■ セルフジャッジ
自分で判断すべきものは自分で判断してください。

上記パフォーマンスに関する働き方やプロジェクトの進捗に対する各種判断等、あなたがジャッジして下さい。

ジャッジをするための相談やサポートが必要な場合も遠慮なく言ってください。

### ■ 結果
ソフトウェア/サービス開発には様々な不確定要素が存在しますが、 **最終的なアウトプット** しかクライアント/ユーザーは見ません。

そこに至るまでの工程や手法は各人が担当している役割等に応じて変わってくると思いますが、仕事の評価はそこに帰結されるのは必然です。

### ■ 責任
セルフジャッジをする以上、対象プロジェクトに対する責任はあなたの手に委ねられます。

おっと、そうは言っても恐れることはありません。最終的には経営陣が責任を取ります。

とにかくあなたは **クリエイターとしての能力** を発揮することに集中してください。


## 働き方について

### ■ 作業開始報告について
作業開始時に作業予定内容（issueやPRのURL）をSlackに流しておくこと。

### ■ 平日に休暇を取る場合
自分の裁量で平日に休暇を取ることに対して特に制約/制限は設けません。

ただ、あなたがお休みでも一般的な日本の会社に勤務しているクライアントは働いていますし、クライアントが国外の場合には日本が祝日でも相手は平日であることもあります。

従って、自分の担当クライアントが働いている日に休暇を取る場合には必ず事前にその旨を共有しておいてください。

仕事は自社だけで完結している訳ではありません。必ずモニターの向こうにユーザー/クライアントがいます。そのことを忘れずに。

### ■ 日報について
Slack上の `#daily-report` にて、作業内容（作業したissueやPRのURL）を報告してください。


## 開発の進め方について

### ■ 開発マシン
社員は付与されたPCを利用しますが、外部パートナーの方は各自のノートPCでも構いません。

### ■ 開発言語
原則的に初期リリースまでにかかる工数が少ないRuby on Railsを利用します。

受託開発案件の場合はクライアントと協議することになりますが、Ruby on Railsを利用しない案件はほぼありません。

#### ◆ バックエンド
Ruby on Rails（2017年4月時点では5.0.2）をそのまま利用しますが、APIのみ提供するプロジェクトの場合にはgrapeと組み合わせて利用することもあります。

コーディング規約については最近のレポジトリであればRubocopを利用してチェックを行っています。

#### ◆ JavaScript
![](http://justdevign.com.au/wp-content/uploads/2014/08/CoffeeScript_Logo_128.png)

JavaScriptを直接記述するのは極力避け、CoffeeScriptで記述します。

##### ▲ スタイルガイド
クラス名/関数名はCamelCaseを基本とします。

```coffeescript
# Good
class HelloWorld

  sayHello: ->
    alert 'hi!'

# Bad
class hello_world
  say_hello: ->
    alert 'hi'
```

#### ◆ テンプレートエンジン
![](http://haml.info/images/haml.png)

[Haml](http://haml.info/)を利用します。

##### ▲ スタイルガイド
'='の後には必ず半角spaceを1つ入れてください。

```haml
-# Good
%p= @variable

-# Bad
%p=@variable
```


#### ◆ スタイリング
![](https://dynamicimagesfr-v2b.netdna-ssl.com/product_class_external_product/sass.png)

SASS（SCSS）で記述します。

CSSのフレームワークとしては[Bootstrap 3](http://getbootstrap.com/)や[Foundation](http://foundation.zurb.com/)を利用します。

![](http://www.w3schools.com/bootstrap/bs.png) ![](http://31.media.tumblr.com/avatar_3865d3a8accc_128.png)

##### ▲ スタイルガイド
[Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.xml)に準拠します。


### ■ ソースコードの管理について

![](http://kykamath.github.io/images/github.png)

[GitHub](https://github.com/)を利用します。

実装を行わない方もissueの登録等でレポジトリを閲覧できる必要がありますので、アカウントを持っていない場合は作成してください。

また、セキュリティレベル向上のためアカウント作成後に[二段階認証](https://help.github.com/articles/about-two-factor-authentication/)を有効にしてください。


### ■ プロジェクトの進捗管理

GitHubのIssue機能を利用して行います。

マイルストーンを週単位で作成した上で、その週に行う予定のissueを登録していきます。

#### マイルストーンの命名規約

```ruby
[
  'v',
  Date.today.beginning_of_week.strftime('%Y%m%d'),
  '-',
  Date.today.end_of_week.strftime('%Y%m%d')
].join ''
# => 例). v20151026-20151101
```

基本的にはスクリプト経由で当週のマイルストーンが作成されていますが、作成されていない場合は上記命名規約に従って作成をお願いします。

#### ◆ issue登録時に設定する項目

##### 件名（Title）
長すぎず、完結に。
```
例). XXXにパスワードリマインダの機能を実装する
```
##### 本文（Comment）
issueを見た人間が開発に取り組めるように、情報が多すぎる位でも問題ありません。

4W1H（What / Why / Where / When / How）を明確にするように記述すると対象機能に関する簡単な議事録としても残せるのでオススメです。

```
例).
## 何を作るのか？
パスワードリマインダーです。

## 何故作るのか？
パスワードを忘れたユーザーにパスワードを再発行するフローを作りたいから。

## どこに作るのか？
同一サービス上の、ログインフォームの下にリンクをつけて誘導する。

## どうやって作るのか？
deviseの機能を使って実装します。

## 作成/変更するテーブル定義
usersテーブルにtemporary_key（string, null: false）を追加

## 参考リンク/資料
- [Google](https://www.google.com)
- [フォームデザイン.pdf](xxx)
```

##### ラベル（Labels）
ラベルについては特に制約は設けませんが、[Waffle](https://waffle.io)を利用して管理していることが多いです。

##### マイルストーン（Milestones）
やることが決まっているものは必ずいつ取り組むのか分かるようにマイルストーンを設定すること。

実装時期が未定だったり、実装自体するか検討中のissueについては「Backlog」マイルストーンを設定してください（なければ作成してください）。

![](https://raw.githubusercontent.com/iro-dori/welcome/master/images/milestones.png)

##### 担当者（Assignee）
担当者が決まっている場合は指定すること。

##### レビュー者（Reviewer）
レビューして欲しい人間のアカウントを指定してください。

### ■ 作業開始から終了まで

基本的にgit-flowの流れに則った形で作業を進めていきます。

参考 : [Understanding the GitHub Flow](https://guides.github.com/introduction/flow/)

- issueに作業内容を登録
- 作業用ブランチ作成
- 実装作業
- GitHubへ作業用ブランチをpush
- プルリクエストの作成
- 実装者以外のレビュー
- （レビューで修正の指定がある場合は修正後、再度レビューを依頼）
- 本ブランチ（主にmaster）へのマージ

プロジェクトメンバーが増えてリリースphaseを踏む形にシフトする際はタイミングをみてGit-Flowへ移行していきます。

#### ◆ 利用するブランチ
初期開発完了（受託開発であれば納品まで。サービスであれば初期ローンチまで）はmasterブランチをmerge先のブランチとします。

issueの対応を行う際にはGitHub-Flowに則り「features/your-task」のような形で新しくmasterからブランチを作成して作業を開始してください。

1つのブランチで複数のissueを対応しても問題ありませんが、多く詰め過ぎるとmergeが面倒になるので最大3つのissueを目処にしてください。

![](http://joefleming.net/images/posts/git-flow-timeline.png)

#### ◆ ローカルでのmergeについて
作業用ブランチにmasterをmergeするタイミングなど、ローカルでmerge作業を行う際には必ず「--no-ff」を指定してください。

```shell
# masterブランチを自分の作業用ブランチにmergeする場合
git merge master --no-ff
```

#### ◆ プルリクエストの作成
作業用ブランチでの作業が完了したら、masterブランチに対してプルリクエストを作成してください。その上でSlack上のプロジェクト用チャネルで

```
@reviewer pull-request-url

レビューお願いします。
```

のような形でSlack上で声をかけてください。

（複数のプロジェクトが同時に進行しているため、GitHub上の作業が流れてしまうのを防ぐためです）

![](https://raw.githubusercontent.com/iro-dori/welcome/master/images/pr-slack.png)

プルリクエストに記述する内容はテンプレートの項目を埋める形にすると楽です。

- このプルリクエストは何なのか？
- どこからチェックし始めればいいのか？（例えば起点/中心となるクラス）
- どうやってテストすればいいのか？
- 実装の背景となることで何か特筆すべきことがあれば記述
- （もしあれば）関連するissue
- スクリーンショット
- 質問事項（実装方針に関することや、いつマージすべきか、など）

参考 : [Pull request templates make code review easier](https://quickleft.com/blog/pull-request-templates-make-code-review-easier/)

#### ◆ issueの完了
gitでcommit時のメッセージとして「fixed #000」と入れておいてください。

こうしておくことで、masterにmergeされた時点でissueが自動的にcloseされます。

自動的にissueをcloseしたくない場合には、「#000」とだけ書いておけばissueに関連づけられます。

![](https://raw.githubusercontent.com/iro-dori/welcome/master/images/issue-log.png)


### ■ テストコードについて
Railsのプロジェクトであればrspecを利用します。ほとんどのプロジェクトでは原則モデルのunitテストだけで十分です。

継続して案件が進む場合には必要に応じて追加します。また、以下のものについてはリリース前までに書いておいたほうが幸せになれることが多いです。

- 決済機能
- API

### ■ コメントについて
クラス単位でのコメントは最小限に（そもそもクラス名を見てその役割が分からないのはおかしいので）とどめる形で構いません。

関数単位でのコメントは

- その関数が行っていること
- 引数の説明
- 戻り値の説明
- その他補足事項

を記述するようにしてください（以下の例を参照）。

```ruby
#
# イロドリの業務に関する処理を記述する
#
class IrodoriCorporation

  #
  # 社員に給料を支払う
  #
  # 何の変哲もないアクションです。
  #
  # @TODO 通貨が変わった場合はどうする？
  #
  # @param [User] user 給料を支払うユーザー
  # @param [Integer] price 支払い金額
  #
  # @return [Boolean] 支払い処理に成功したらtrue、失敗したらfalse
  #
  def paySalary(user, price)
    # ...
  end
end
```

### ■ ドキュメンテーションについて
設定や備考録等、対象プロジェクトに関するドキュメントはGitHubのWikiにまとめてください。

無理やり1ページに納める必要はないので、Homeページからリンクを貼る形で機能/項目単位でページを作成して問題ありません。
