---
marp: true
theme: gaia
paginate: true
footer: 2020/01/08 Marp Cliの使い方
style: |
    section {
        font-family: 'Noto Sans JP';
        color: black;
        font-size: 20px;
    }
    h1 {
        font-size: 34px; 
    }
    h2 {
        font-size: 30px; 
    }
    h2 {
        font-size: 24px; 
    }
    section.lead h1{
        font-size: 60px;
    }

---

<!-- _class: lead -->

# Marp Nextで頑張る
## お試しファイルです

---

# インストールから表示まで

旧: Marp
新: [Marp Next](https://tech.speee.jp/entry/2019/08/01/173843)
Marptit フレームワークとMarp Core2つの核となるモジュールがある
今からやるのは[Marp CLI](https://github.com/marp-team/marp-cli)という、Marpアプリケーションの一種で、Node.jsをインストールしてスライドをWebページで公開できるもの

参考サイト
- [M3テックブログ](https://www.m3tech.blog/entry/marp-cli#fn-5058435a)
- [Marpit Markdown](https://marpit.marp.app/markdown)


----
# 基本的にエムスリーテックブログと同じ
<br>

1. まずはnode.jsをインストールする
node.jsってなに
→ フロントエンド言語であるjavascriptをサーバーサイドにも使えるようにした言語
2. スライドを置くディレクトリを作成し、`package.json`を作成する

----
marpのバージョンだけ最新版に変えた(`dependencies`のところ)
```
{
  "name": "my-slide",
  "version": "1.0.0",
  "main": "index.js",
  "author": "作者名",
  "license": "UNLICENSED",
  "private": true,
  "scripts": {
    "dev": "marp --html --server .",
    "build": "marp --html --pdf --allow-local-files --title 'スライドのタイトル' slide.md -o ./slide.pdf"
  },
  "dependencies": {
    "@marp-team/marp-cli": "^0.16.2"
  }
}

```
---
3. `＄ yarn install`を実行する
自分はnode.jsをインストールしたのに`command not found`って
言われたから`$ brew install yarn`した
4. エディタVSコードでマークダウンファイルを記述する
[Marp for VSCode]プラグインをダウンロード
スクショで画像を貼り付ける際は
    1. 拡張機能「Paste Image」をダウンロード
    2. Ctrl + Shift + Command + 4 で範囲選択してスクショ取得&クリップボードに取り込み
    3. Option + Command + v でmarkdownファイル中に貼り付け
    →同じディレクトリに画像が勝手に保存されている
    [画像のサイズ指定など](https://marpit.marp.app/image-syntax)
    今の所Markdownで真ん中寄せにするには`<div align='center'></div>` と書くしかなさそうだけどMarpでやるのかどうやるのかわからない
    https://qiita.com/takkii/items/d09668cbf85cbdec7001

        ![width:500px](2020-02-26-11-03-55.png)

---

5. コマンドで`$ yarn dev`を実行
localhost:8080でスライドがみれる
![width:500px](2020-02-26-11-27-00.png)

<br>
右上の「PDF」「PPTX」でスライドをダウンロードすることも可能

でもPPTXはテキスト部分等編集できない！スライドは分かれてるけど！残念！

---
# メモ
コマンド`npx`を使ってインストールする方法もあるけど
package.jsonで記述してMarpCLIを導入する利点として
```
- npx で毎回起動すると遅い点
- dependencies でのバージョン指定はしておいたほうが良い点
- package.json の scripts にコマンドを記述しておいたほうがシンプルである点
```
システム全体にインストールされるのではなく、特定のディレクトリ配下にMarpCLIがインストールされる利点として
```
- プレゼンテーションごとに異なるバージョンの marp (や marp の依存ライブラリ)を利用できる
 Marp やそれが依存する JavaScript ライブラリは開発が活発ですし、過去に作ったスライドを最新版で開いたら変なことに...という事態を回避する意味で重要です

- package.json と同じ階層の node_modules 以下に配置されるだけなので、管理者権限が不要 & システムの環境が汚れる心配もない

(Git を使う場合、 node_modules/ は .gitignore に指定した方が良いです。)
```

----
<!-- _backgroundColor: white -->
# Directives
スライドの書式の宣言等の仕方。

1. Global directives: 全体に適用される。スライドマスターみたいなもの
```
<!-- backgroundColor: white -->
# Directives
スライドの書式の宣言等の仕方。

1. Global directives: 全体に適用される。スライドマスターみたいなもの

---

2枚目以降のスライドにも適用される

```

2. Local directives: 各ページに適用される
```
<!-- _backgroundColor: white -->
先頭に`_`をつける
# Directives
スライドの書式の宣言等の仕方。

---

2. Local directives: 各ページに適用される

```

---
# Directives

今使ってるスライドのテーマは`theme:gaia`だけど、デフォルトだと文字が大きすぎたので自分でカスタマイズ。
以下コピペで最初にGlobal direvtiveとして宣言する。
```
---

marp: true
theme: gaia
paginate: true
footer: 2020/01/08 Marp Cliの使い方
style: |
    section {
        font-family: 'Noto Sans JP';
        color: black;
        font-size: 20px;
    }
    h1 {
        font-size: 34px; 
    }
    h2 {
        font-size: 30px; 
    }
    section.lead h1{
        font-size: 60px;
    }

---

```
https://marpit.marp.app/directives?id=global-directives

---

- Marpでは、各スライドがHTMLでいう`<section>`要素と名付けられている. 
あるスライドの特定の属性(例えば大見出しh1)だけ, フォントサイズなど変更したかったら
```
section.クラス名 h1{
  font-size:40px;
}
```
のように指定する。書き方自体はcssと同じ。

---

# 使いかたもろもろ

- 絵文字はエイリアスで使えるの知らなかった:bow::+1:
- TeXで数式を書く
> $$ c^2 = a^2 + b^2

$$ \vec{a} + \vec{b} = \vec{c} $$
数式は正直難しいけどパワポのGUIで数式をいちいち選択するより楽なはず


----
# 使いかたもろもろ
- 絵文字はエイリアスで使えるの知らなかった:bow::+1:
- TeXで数式を書く
> $$ c^2 = a^2 + b^2

$$ \vec{a} + \vec{b} = \vec{c} $$
数式は正直難しいけどパワポのGUIで数式をいちいち選択するより楽なはず

アニメーションはできなさそうだけど同じ文章をコピペすることでアニメーションっぽくすることは可能そう
<br>
<br>

---

# どう使うか
<br>

### メリット
- レイアウトを全く気にしなくていい. 図とか文字を画面凝視しながら絶妙に配置しなくて済む。
- LateXをそのままかけるので数式をストレスなく挿入できる
- コードブロックが書ける. ハンズオンに最適？特にエンジニア同士の勉強会でかなり使われている模様
<br>

### デメリット
- 細かい微調整は無理なので凝ったスライドやプレゼンテーションはできない
- MarkdownやHTML, CSSに慣れていないと手こずって逆に時間かかるかも
<br>

### どんな時に使えるか
- 自分のメモをそのままみんなに資料として見せたいとき
- ゼミ資料を凝らずにパパッと作り上げたいとき
つまり勉強内容をそのままMarpでアウトプットすれば効率いいかもしれない