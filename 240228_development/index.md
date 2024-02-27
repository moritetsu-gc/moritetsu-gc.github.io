# htmx
## - JavaScriptの記述なしでAjax通信が可能に！？ -
2024.2.28.(Wed.) 技術情報共有会
T.Morinaga

![htmx](https://raw.githubusercontent.com/bigskysoftware/htmx/master/www/static/img/htmx_logo.1.png)

---

## htmxとは
* HTMLの記述だけでJavaScriptの処理を実行可能
  * Ajax
  * フォーム送信
  * DOM処理
* 昨年後半から欧米では話題になっているらしい

### 参考
* 公式サイト： https://htmx.org/
* 詳しい記事： https://qiita.com/twrcd1227/items/7bce18167fb02ec22729

---

## 始めてみましょう
* unpkg.comからダウンロードしてscriptタグでロード。
  * CDNもあるが本番環境での使用は非推奨とのこと
  * https://blog.wesleyac.com/posts/why-not-javascript-cdn

```
<script src="/path/to/htmx.min.js"></script>
```

* もちろんnpm installで入れることも可能

```
npm install htmx.org
```

---

## 簡単な使い方
### Ajax
* hx-(method)=(url) 属性を追加すれば可能
```
<div hx-get="/messages">hoge</div>
```

---

### ターゲット
* hx-target=(セレクタ) でターゲット要素を指定可能

### イベント発火
* hx-trigger=(イベント名)

```
<button hx-get="/example" hx-target="#target" hx-trigger="click">クリック</button>
```

---

## できること
* Ajax(get/post/etc...)
* DOM操作(Ajaxで取得したデータを指定の要素に表示)
* イベント発火(click/change/etc...)
* アニメーション
* history
* ダイアログ(confirm)
* バリデーション

---

### 拡張機能もあり
* https://htmx.org/extensions/
* 用意されている機能拡張
  * client-side-templates：JSONで受け取ったデータを展開するテンプレート
  * class-tools：CSSのクラス追加/削除のタイミング操作 → アニメーションに便利
  * 他にもたくさんあります

#### 使い方
```
<script src="/(path)/(extention).js" defer></script>
<button hx-post="/example" hx-ext="(extention)">This Button Uses The Extension</button>
```

* さらに自作も可能(→さすがにこれはJavaScriptを使います)

---

## サンプル
* 公式のサンプル集： https://htmx.org/examples/

---

## 所感
* JavaScriptを一切書かずにいろいろなインタラクティブ処理を行えるというのは画期的だと感じました
* ただ、行える処理はあくまで限定的でJavaScriptの処理全てができるわけではない
  * 例えば演算処理
  * そのあたりは既存のライブラリ/フレームワークと上手く組み合わせれば世界が広がる(かも)
* 「ロジックとテンプレートが密結合しやすい」という指摘あり
  * 記事→ [htmx: 新しい Web 開発のトレンド - htmxのデメリット](https://descarty.com/blog/htmx-introduction/#htmx-%E3%81%AE%E3%83%87%E3%83%A1%E3%83%AA%E3%83%83%E3%83%88)
  * 確かに複雑なシステムになるとロジック部分が分離していないので可読性が落ちやすそう
  * シンプルなページ/システム向き？
