---
marp: true
theme: gaia
paginate: true
footer: 2020/01/08 Marp Cliの使い方
---

<!-- _class: lead -->
# Marp Nextで頑張る

---

# インストールから表示まで

[M3テックブログ](https://www.m3tech.blog/entry/marp-cli#fn-5058435a)
[Marpit Markdown](https://marpit.marp.app/markdown)
[Marp CLI 公式サイトらしきところ](https://www.npmjs.com/package/@marp-team/marp-cli)

----
基本的にエムスリーテックブログと同じ
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

4. エディタVSコードでマークダウンファイルを記述する<br>
[Marp for VSCode]プラグインをダウンロード
スクショだと画像のサイズ変更ができない悩み....

![image](https://user-images.githubusercontent.com/49149391/71904343-3fedbb00-31a9-11ea-83d3-8db67f5b526d.png)

---

5. コマンドで`$ yarn dev`を実行すれば、localhostでスライドがみれる

![image](https://user-images.githubusercontent.com/49149391/71904834-39137800-31aa-11ea-8794-5d3feacd05b4.png)

右上の「PDF」「PPTX」でスライドをダウンロードすることも可能
でもPPTXはテキスト部分等編集できない！なんやねん！

---
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

---

## 使いかた

- 絵文字はエイリアスで使えるの知らなかった:bow::+1:
- TeXで数式を書く
> $$ c^2 = a^2 + b^2

$$ \vec{a} + \vec{b} = \vec{c} $$
数式は正直難しいし、図とか作るならやっぱりパワポかなぁ。


----
## 使いかた
- 絵文字はエイリアスで使えるの知らなかった:bow::+1:
- TeXで数式を書く
> $$ c^2 = a^2 + b^2

$$ \vec{a} + \vec{b} = \vec{c} $$
難しい。

アニメーションはできなさそう

----
## 使いかた
- 絵文字はエイリアスで使えるの知らなかった:bow::+1:
- TeXで数式を書く
> $$ c^2 = a^2 + b^2

$$ \vec{a} + \vec{b} = \vec{c} $$
難しい。

アニメーションはできなさそう
でも同じ文章をコピペすることでアニメーションっぽくできそう



