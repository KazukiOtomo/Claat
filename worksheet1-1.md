author: Kazuki Otomo
summary: WorkSheet1-1
id: WorkSheet1-1
categories: codelab,markdown
environments: Web
status: Published
feedback link: https://github.com/KazukiOtomo

# ソフトウェアデザイン第10回

## はじめに
これから3回の講義にわたって、皆さんには情報システム設計の一端を経験してもらいます。
まずは、現状の知識を活用してブラックジャックを作ってみましょう。

<aside class="negative">
1回分の課題としてはかなり重い課題だと思います。自分の納得できるところまで取り組んでもらえると、よりこの後の講義で得られるものが多くなると思います。
</aside>

## 仕様について
フロント部分についてはLineBotを利用し、データベースも使います。
ゲームのルールについては、ローカルルールなど複数あるようなのでこちらから指定します。
記述されていないルールに関しては、各々の判断に委ねます。
任意でクラス図やビジネスフロー図などの図を使っても構いません。

 - プレーヤーとディーラーは、最初にカードを2枚ずつ引く
 - ディーラーはカードを１枚だけ公開しておく
 - それぞれの初期手札をデータベースに記録しておく（テーブル構造の定義については指定はありません）
 - 10以上のカード（J, Q, K）は、全て「10」として扱う
 - 1（A）については、そのまま「1」として扱う
 - ディーラーは手札が「17」以上になるまでカードを引かなければならない
 - 手札の合計値が「21」に近い方の勝利
 - 手札の合計値が「21」を超えると失格
 - 引き分けの場合はディーラーの勝ちとする（両方失格、手札の合計値が同じの場合はディーラーの勝利）

イメージ画像（表示のメッセージについて指定はありません）
![LINEBot参考画像](png/eDwerkWF.jpeg)



## Giuhub ClassRoomへのPush

### commit コマンド

```
git add.
git commit -m "10回目の課題ファイルを追加"
git push
```
課題が、課題提出場所（リポジトリ）のURL https://github.com/cist-ictdev-2022/git-test-xxxxxx に提出されます。

課題提出場所（リポジトリ）のURL https://github.com/cist-ictdev-2022/git-test-xxxxxx をもう一度ブラウザで開き、課題のファイルが提出（push）されていることを確認する。

ここまで終われば完了です。お疲れ様でした。

## 環境構築（一応）

### IntelliJ IDEA Ultimateの準備
IntelliJ IDEA Ultimate を使います。

IntelliJ IDEA Ultimate は学生の間、学生アカウントで1年間無料で利用できます。

**すでにインストールされている場合**<br>
Intellij IDEA Ultimateを最新版（バージョン　2022.2.3）に更新してください

Windowsの場合は、ファイルメニューの　ヘルプ > アップデートの確認（check for Updates…​)

macOSの場合は、ファイルメニューの IntelliJ IDEA > Check for Updates…​

**Community版を利用している、再インストールしたい、PCを新しくしたなどの事情がある場合**<br>
以下の資料を参考に、IntelliJ IDEA Ultimateを新インストールしてください。<br>
[https://github.com/cist-ictdev-2022/InstallIntelliJ/blob/main/README.md](https://github.com/cist-ictdev-2022/InstallIntelliJ/blob/main/README.md)

### LineBotの準備
（ソフトウェア工学概論と同じもの）<br>
環境が既に整っている場合は飛ばしてください。<br>
[https://cist-ictdev-2022.github.io/SoftEng22/02a_InitProject/#0](https://cist-ictdev-2022.github.io/SoftEng22/02a_InitProject/#0)

### H2DBの準備
（ソフトウェア工学概論と同じもの）<br>
データベースファイルの名前はお任せします。（忘れないようにだけ気をつけてください）<br>
[https://cist-ictdev-2022.github.io/SoftEng22/02b_DBSettings/#0](https://cist-ictdev-2022.github.io/SoftEng22/02b_DBSettings/#0)
