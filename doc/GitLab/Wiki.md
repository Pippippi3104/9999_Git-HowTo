# Wiki of GitLab

<a id = "contents">

# Contents
* [macでgitlabにSSHキーを登録する](#macでgitlabにSSHキーを登録する)

### Pickup
* [【GitLab】プロジェクト（リポジトリ）を作成する](https://qiita.com/CUTBOSS/items/ce61bb6a8635c6918558)
* [【Git】macでgitlabにSSHキーを登録する【SSHキー複数管理】](http://www.rikyu-sen.com/entry/git-add-ssh)


<a id = "flow">

## FlomacでgitlabにSSHキーを登録する
<!-- * ![Image](../src/Section07/images/init001.png) -->

* commands
  * SSHキー作成
    * パスフレーズを求められるが今回はEnterでスキップ
    * gitlabという名前で作った
  ```
  mkdir ~/.ssh
  chmod 700 ~/.ssh
  ```
  ```
  ssh-keygen 
  Generating public/private rsa key pair.
  Enter file in which to save the key (/Users/username/.ssh/id_rsa): 好きなファイル名をここに入力(今回はgitlabで作成)
  Enter passphrase (empty for no passphrase): 
  Enter same passphrase again: 
  ```
  * SSHキーの管理
  ```
  cd ~/.ssh
  vim config
  ```
  ```
  # gitlab これはコメント
  Host gitlab.com
    User ユーザ名（今回はgitlabのユーザ名で良い）
    HostName gitlab.com
    identitiesonly yes
    identityFile ~/.ssh/gitlab (←上記で作成した鍵のパス)
  ```
  * gitlabへの鍵登録
    * これでクリッピボードに鍵の中身がコピー
  ```
  cd -/.ssh
  pbcopy < gitlab.pub (上記で作成した鍵の.pubをクリップボードにコピーしている)
  ```

### [Return to Contents](#contents)