# Gitの環境構築

## Gitとは
Gitはソースコード管理ツールです。ファイルを編集前の状態に戻したり、チームで同時に同じファイルを編集できたりなど現代のソフトウェアのソースコード管理では必須となっています。

## 手順
### Githubの登録
1. [Githubのサイト](https://github.co.jp/)にアクセス
2. [GitHubアカウントの作成方法 (2021年版)](https://qiita.com/ayatokura/items/9eabb7ae20752e6dc79d)を参考にアカウントを作成する

### Gitの環境構築
使用しているOSによって該当するサイトのページを確認し、それにしたがってセットアップをしてください。

#### Windows
`①Gitのインストール` と `②Gitの初期設定` まで行なってください。それ以降は必要ありません。

[【Windows】Gitの環境構築をしよう！](https://prog-8.com/docs/git-env-win)

#### Mac
`①環境構築の準備` と `②Gitのインストール` 、 `③Gitの初期設定` まで行なってください。それ以降は必要ありません。

[【Mac】Gitの環境構築をしよう！](https://prog-8.com/docs/git-env)

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

## 大学内でGitを使用するとき
- 大学内でGitをリモートに接続して使うときは proxy の設定をしないと使えないので注意してください。
- proxy 設定をしたら、解除コマンドを打たない限り自宅などでGitを使えなくなるので注意！

```bash
# proxy設定
$ git config --global http.proxy wwwproxy.kanazawa-it.ac.jp:8080

# proxy解除
$ git config --global --unset http.proxy
```

## Gitの理解に参考になるサイト
[サルでもわかるGit入門](https://backlog.com/ja/git-tutorial/)
