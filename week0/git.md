# Git の環境構築

## Git とは

Git はソースコード管理ツールです。ファイルを編集前の状態に戻したり、チームで同時に同じファイルを編集できたりなど現代のソフトウェアのソースコード管理では必須となっています。

## 手順

### Github の登録

1. [Github のサイト](https://github.co.jp/)にアクセス
2. [GitHub アカウントの作成方法 (2021 年版)](https://qiita.com/ayatokura/items/9eabb7ae20752e6dc79d)を参考にアカウントを作成する

### Git の環境構築

使用している OS によって該当するサイトのページを確認し、それにしたがってセットアップをしてください。

#### Windows

`①Gitのインストール` と `②Gitの初期設定` まで行なってください。それ以降は必要ありません。

[【Windows】Git の環境構築をしよう！](https://prog-8.com/docs/git-env-win)

#### Mac

`①環境構築の準備` と `②Gitのインストール` 、 `③Gitの初期設定` まで行なってください。それ以降は必要ありません。

[【Mac】Git の環境構築をしよう！](https://prog-8.com/docs/git-env)

## 主なコマンド

```bash
$ git clone                   #既存のgitリポジトリのコピーを取得したい場合に使う
$ git init                    #「.git」というリポジトリを構成するディレクトリを作成

$ git add                     #追加されたファイルなどをGit管理の対象に入れる

$ git commit                  #ファイルの変更をgitレポジトリに保存
$ git merge                   #別ブランチの変更を統合

$ git pull                    #リモートをローカルに反映
$ git push                    #コミットした内容を反映

$ git                         #gitコマンド一覧を表示
$ git diff                    #変更内容を確認
$ git log                     #ログを見る
$ git status                  #現状の確認

$ git branch                  #ブランチの確認
$ git branch [ブランチ名]       #ブランチの作成
$ git checkout [移動先]        #ブランチの移動
$ git checkout -b [ブランチ名]  #ブランチを作りながら移動
```

## 大学内で Git を使用するとき

- 大学内で Git をリモートに接続して使うときは proxy の設定をしないと使えないので注意してください。
- proxy 設定をしたら、解除コマンドを打たない限り自宅などで Git を使えなくなるので注意！

```bash
# proxy設定
$ git config --global http.proxy wwwproxy.kanazawa-it.ac.jp:8080

# proxy解除
$ git config --global --unset http.proxy
```

## Git の理解に参考になるサイト

[サルでもわかる Git 入門](https://backlog.com/ja/git-tutorial/)
