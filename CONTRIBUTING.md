# Contribution Guide

## プルリクエストについて

何のために何を作る（作った）のか？を明示的にしておく必要があります。  
プルリクエストの内容がしっかりしていると、開発中はガイドラインとして、開発後は経緯として組織の助けとなります。  
巨大なプルリクエストにならない様に注意してください。

## プルリクエストの作成

**緊急対応等、出すことを優先する場合はこの限りではありません。但し、書かなくて良い訳ではないので対応後にWhyとWhatの記述をお願いします。**  
WIPプルリクエスト方式を採用しています。（Draft Pull Requestでなければならないわけではありません）。  
開発を始める際、以下の流れでプルリクエストを作成してしまいます。

### 手順

1. 親ブランチから開発ブランチを作成する
1. 空のコミットを作る
1. remoteへpushする
1. GitHubへアクセスし、開発ブランチから親ブランチに対してプルリクエストを作成

```sh
git checkout -b <開発ブランチ名>
git commit --allow-empty -m 'プルリクエストのタイトル'
git push origin <開発ブランチ名>
```

#### プルリクエストのタイトルについて

チケットがある場合は、チケット番号やIDをプレフィクスとしてつけます。  
後から検索しやすくすることが目的です。

### プルリクエストの内容

プルリクエストで情報を完結させることを目的としています。  
以下をConversationに書いてください。

#### Ticket（必須）

該当チケットのURLを記述します。  
チケットなしの場合は `なし` と記述します。

#### Why（必須）

プルリクエストが出された背景を記述します。  
どうして変更が入ることになったかを明示的にしておくことで、後日変更の意図を追うことができる様になります。  
プルリクエストにWhyを書くことで、背景や目的について再考することも目的の一つです。

#### What（必須）

プルリクエストがマージされることで何ができるようになるかを記述します。  
何を達成しなければならないかを明示的にしておくことで、開発中のガイドラインになります。シーケンス図などといった図や、画面に関することであれば変更前後のスクリーンショットなども確認できる様にしておきます。  
また、場合によっては当該プルリクエストでは行わないことなどを記述しておくことも有用です。

#### レビューポイント（任意）

レビュワーに特に確認してほしい点について記述します。  
レビュワーの負担軽減にも繋がります。  
不安な点があればレビュー時ではなく実装時に相談しましょう。

#### TODO（必須）

開発しなければならないことをチェックボックス形式で記述し、実装が終わるたびにチェックを入れます。  
*（具体的なクラス名やメソッド名ではなく、何を達成したいのか単位での記述を推奨します）*

開発中、やるべきことが増えた場合は追記していきます（機能追加などの要件が増えたといった場合だけではなく、気づいたことなども含みます）。  
TODOを明示的にしておくことで、全体像や何が未実装なのかといったことが分かる様になります。  
また、コミットメッセージをTODO単位にすることでレビューのしやすさ、rebaseのしやすさが向上します。

TODOはネストさせることが可能ですが、最終的なコミット単位は親のTODOにするとまとまったコミットとなり分かりやすいです。

#### その他（任意）

項目名はなんでも構いません。  
プルリクエストに残しておくべき補足情報があれば記述します。

#### 関連するPR（任意）

プルリクエストのURLを記述します。  
関連しているプルリクエストが存在する場合は **必須** になります。

## コミットメッセージについて

どういった変更を加えたかを説明するという重要な役割があります。

## コミットメッセージの書き方

`タイトル` と `説明` に分けて記述します。  
タイトルと説明の間には、空行を1行追加します。
```
タイトル

説明
```

### タイトル

プルリクエストのTODOと一致させることを基本とします。  
[Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)に従いタイプを設定することを推奨しますが、後に `rebase -i` でまとめてしまうコミットについてはその限りではありません。  
`rebase -i` でまとめるコミットの例は、ネストされたTODOの子であったり、レビュー指摘の修正コミットなどです。  
TODOに当てはまらないコミットの場合、要点を簡潔に伝えるタイトルにします。  

### 説明

タイトルだけでは伝えられない詳細を記述します。後でコミットを見た時に、開発時に考えていたことが伝わる様にしましょう。  
また、詳細を書くことはレビューの助けにもなります。

複数記述する場合はリスト形式（markdown）で書く様にします。  
子TODOなどは記述の対象です。

## コンフリクトしたコミットについて

取り込みの順番によってはコンフリクトが発生する場合があります。  
開発中に大幅な方針転換をしたリファクタリングの様なケースや、同じ部分の修正を分割して行っている場合などに起こりやすいです。  
あまりにも修正するのに時間がかかる様なコンフリクトの場合は別コミットとしてしまって構いませんが、もし発生してしまった場合はレビュワーに相談をして決めましょう。

## レビュー指摘の修正コミットについて

基本的に1つのコメントに対し1つの修正コミットとします。  
そうすることで何を修正するか（したか）が明示的になり、開発者及びレビュワーどちらにもメリットがあります。  
但し、複数箇所で指摘されている同一内容のコメントなどは例外です。  
レビュー指摘の修正コミットは、レビューが完了したら `rebase -i --autosquash` にてまとめてしまい、履歴に残さない様にします。  
以下の点がわかる様にコミットメッセージを設定します。

1. どのコミットにまとめるか分かる様にする
1. どのレビューコメントに対する修正か分かる様にする

### どのコミットにまとめるか分かる様にする

レビュー完了後相応しいコミットにまとめるために、特別なプレフィクスをコミットメッセージのタイトルにつけます。  
これらのプレフィクスを自動でつけるには、コミット時にどのコミットにまとめるつもりなのかを指定する必要があります。

- **fixup!** : コミットメッセージを変更することなくまとめたい場合に利用します。

  例) `doc: Pull RequestのConversationに残すべきことについて` というコミットにまとめたい場合は、下記の様になります。
  ```
  git commit --fixup 'doc: Pull RequestのConversationに残すべきことについて'  #リビジョンやHEAD指定もできます

    -> fixup! doc: Pull RequestのConversationに残すべきことについて
  ```
- **squash!** : まとめたコミットのメッセージを変更したい場合に利用します。
  例) `doc: Pull RequestのConversationに残すべきことについて` というコミットにまとめたい場合は、下記の様になります。
  ```
  git commit --squash 'doc: Pull RequestのConversationに残すべきことについて'  #リビジョンやHEAD指定もできます

    -> squash! doc: Pull RequestのConversationに残すべきことについて
  ```

### どのレビューコメントに対する修正か分かる様にする

どのレビューコメントに対して修正したかが分かりやすくなる様に、コミットメッセージの説明に「コメントのURL」や「判別しやすいコメント」を記述します。  
また、まとめた時にコミットメッセージに追記したい内容があれば記述しておき、 squash! で後から編集できる様にしておきます。

### リベースのタイミングについて

リベースをしてコミットをまとめると、コメントがなくなってしまう場合があります。  
レビュー指摘のコミットをリベースする際は、レビュー完了後に実施してください。

### リベースにあたっての注意事項

リベースを行うとコミットリビジョンが変わります。（ `-i` をつけるつけない関わらず）  
そのままプッシュはできないのでフォースプッシュが必要になりますが、その名の通り強制的なプッシュとなるため、デグレを引き起こす場合があります。  
これを防ぐために `--force-with-lease` オプションを利用します。  
```
git push --force-with-lease origin <branch>
```

但し、 このオプションも**完璧ではありません**。  
特に `-i` をつけないリベースの場合は注意が必要です。リベース前に、必ずリベース指定するブランチ（親ブランチ）を最新化してからリベースを行ってください。  
親ブランチがmain（master）であればそのままプルすれば良いですが、ブランチを作っている場合は一度削除してmainでプルしてからの方が失敗しないです。  
```
git checkout main
git branch -D <親ブランチ>
git pull
git checkout <親ブランチ>
git checkout <開発ブランチ>
git rebase <親ブランチ>
git push --force-with-lease origin <開発ブランチ>
```

