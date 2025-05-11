author: Kazuki Otomo
summary: Git&Github の使い方
id: github-starter
categories: codelab,markdown
environments: Web
status: Published
feedback link: https://github.com/KazukiOtomo

# 開発現場で困らないための Git & Github

## 案件に配属されました！開発環境を整えましょう！

### 1. レポジトリの URI を取得する

<aside class="negative">
アカウント作成やログインに関しては、Github Docs(https://docs.github.com/ja/get-started/start-your-journey/creating-an-account-on-github)を参考にしてください。
</aside>

<aside class="negative">
最近のGithubはセキュリティ面の強化により、2FAやアクセストークンの発行が必要です。詳しくはGithub Docs(https://docs.github.com/ja/get-started/start-your-journey/creating-an-account-on-github)を参考にしてください。
</aside>

以下画像のボタンから、レポジトリの URI を取得できるのでコピーします。

![レポジトリのURIを取得](png/github1.png)

### 2. **忘れにくい場所**にレポジトリを clone する

以下のコマンドを実行します。

```sh
# ※1. レポジトリのURIは、実際に取得したものに置き換えてください。
# ※2. 「$」 は、コマンドプロンプトのプロンプトを表しています。実行する際は、コマンドプロンプトのプロンプトは入力しないでください。

# 「pwd」（自分のいる場所を確認する）、「ls」（ディレクトリ内のファイルを確認する）などのコマンドを使って、cloneする場所を確認してください。
$ git clone <レポジトリのURI(ペースト)>
```

<aside class="negative">
VSCodeやJetBrains系統のIDEを使っている場合は、IDEのGUIでcloneすることもできます。
ただ、裏でどういうコマンドが動いているかを知っておくことは大切なので、ここではコマンドラインでの操作を紹介しています。
</aside>

### 3. clone したレポジトリを開く

クローンしたものを、VSCode や IntelliJ IDEA などの IDE で開きます。
これで、開発環境の準備は完了です！

![クローンしたものを開く](png/github2.png)

## 仕事です！指示された変更を加えてみましょう！

### 1. ブランチを切る

## あっ！間違ったブランチに commit してしまった！どうすればいい？

## Pull Request を作りましょう！ん？コンフリクトが発生してマージできない？

## 他の人のコードレビューをしてみましょう！
