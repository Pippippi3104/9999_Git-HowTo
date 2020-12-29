# Wiki of GitLab

<a id = "contents">

# Contents
* [利用する5種類のブランチ](#利用する5種類のブランチ)

### Pickup
* [git-flow 図解](https://qiita.com/ohnaka0410/items/7c7fa20710dfd72b7d7a)


<a id = "利用する5種類のブランチ">

## 利用する5種類のブランチ
* ![Image](images/branch001.png)

### メインブランチ : 開発の軸となるブランチ
* master ブランチ
  * 分岐元：なし
  * マージ先：なし
  * ブランチ名の例：master
  * 特徴
    * 本番にリリースできる状態を保つ
    * 直接コミットは行わない
    * release 、hotfix からマージを行い、タグを作成する
    * タグ名は release/vX.X.X がよいと思う

* develop ブランチ
  * 分岐元：master
  * マージ先：なし
  * ブランチ名の例：develop
  * 特徴
    * 開発中の最新状態を反映する
    * 基本、直接コミットは行わない
    * feature , hotfix からマージを行う

### サポートブランチ : メインブランチでの開発を補助するためのブランチ
* feature ブランチ
  * 分岐元：develop
  * マージ先：develop
  * ブランチ名の例：他のブランチ名のルールと重複しないもの
    * シンプルに feature/X か、
      feature/YYYYMM_{案件名}/* とかするのがいいと思う
    * Githubなどを用いてissueと合わせて運用するのであれば、
      feature/{issue番号}__X とか、feature/YYYYMM_{案件名}/{issue番号}__X としたほうがいいと思う
  * 特徴
    * 新機能の開発を行うのに用いる
    * develop へマージする際は、Gitの -no-ff オプションも活用する
      (一連のコミットを1コミットにまとめる機能)
    * リモートへPushせず、ローカルでのみ利用する
      * Pull Requestも活用するのであれば、Pushしてもいいと思う

* release ブランチ
  * 分岐元：develop
  * マージ先：master と develop
  * ブランチ名の例：release-*
    * release/vX.X.X がいいと思う
  * 特徴
    * リリースの準備作業を行うのに用いる
      * バージョンの変更
      * 小さなバグフィックス
    * master へマージ後、 develop へマージする
      完了後、release を削除する

* hotfixブランチ
  * 分岐元：master
  * マージ先：master と develop
  * ブランチ名の例：hotfix-*
    * hotfix/* がいいと思う
    * Githubなどを用いてissueと合わせて運用するのであれば、
      hotfix/{issue番号}__* としたほうがいいと思う
  * 特徴
    * 緊急のバグフィックスを行うのに利用する
    * master へマージ後、develop へマージする
      完了後、hotfix を削除する
      * 利用用途としては release に似ているが、
        develop を経由せずに master へマージできるため
        進行中の開発が影響を受けにくい

### [Return to Contents](#contents)