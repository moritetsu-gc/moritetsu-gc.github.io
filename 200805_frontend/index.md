フロントエンド社内勉強会(1)

# 疑似要素!!<br>劇的ビフォーアフター

2020/08/05(Wed.) T.Morinaga

(2020/08/31 改訂)

---

## 内容
* はじめに
* 疑似要素とは
* なぜ必要？
* 似て非なる「疑似クラス」
* 実例
* 使用上の注意
* まとめ

---

## はじめに
* 社内勉強会でやって欲しい内容を募集

![イラスト](illust1.png)

>>>

### 挙がったもの
* 疑似要素(::before、::after)<br>　→ 第1回
* AMP<br>　→ 第2回

---

## 疑似要素とは
* https://developer.mozilla.org/ja/docs/Web/CSS/Pseudo-elements
* セレクターに付加するキーワード
* 選択された要素の特定の部分に(CSSで)スタイル付けできるようにするもの

---

### ::before疑似要素
* 要素の最初の部分に付加
```
<p>あいうえお</p>
```
```
p::before {
    content: '★';
    color: red;
}
```
* 上記の例の場合「あ」の前に疑似要素が入る
![結果](sample1.png)
* [コードサンプル](sample1.html)

---

### ::after疑似要素
* 要素の最後の部分に付加
```
<p>あいうえお</p>
```
```
p::after {
    content: '●';
    color: blue;
}
```
* 上記の例の場合「お」の後に疑似要素が入る
![結果](sample2.png)
* [コードサンプル](sample2.html)

---

## なぜ必要？
### 疑似要素がない場合

```
<p>
    <span class="before">★</span>
    あいうえお
</p>
```

>>>

疑似要素がないとどうなるか？
* HTMLの中身がカオスになる
* 場合によってはSEOに影響する(とも言われている)

---

## 似て非なる「疑似クラス」

:hover、:first-childなど

* 疑似要素<br>
  選択された要素の**特定の部分にスタイル付け**する
* 疑似クラス<br>
  選択された要素に対して**特定の状態を指定**する

---

### ここでちょっと疑問
#### 「:」は1つ？2つ？

* CSS2では1つ、CSS3では2つという仕様
* ただしブラウザではどちらでも同様に解釈
* 要するに(今のところは)表示するだけならどちらでも差異はない
* ただし疑似クラス(こちらはコロン1つ)との区別のため**2つが推奨されている**

---

## 実例
### その1：箇条書きリストのマーカーを任意の記号に

* HTML
```
<ul>
    <li>あいうえお</li>
    <li>かきくけこ</li>
    <li>さしすせそ</li>
</ul>
```

>>>

* CSS
```
ul {
    list-style: none;
}
li {
    padding-left: 1em;
}
li::before {
    content: '★';
}
```

>>>

* 結果

![結果](sample3.png)

* [コードサンプル](sample3.html)

---

### その2：吹き出し

* HTML
```
<div>
    <span>にゃー</span>
</div>
```

>>>

* CSS
```
div {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 70px;
    height: 40px;
    position: relative;
    background-color: #66c;
}
div::after {
    content: '';
    position: absolute;
    top: 100%;
    left: 50%;
    margin-left: -15px;
    border: 15px solid transparent;
    border-top: 15px solid #66c;
}
span {
    color: #fff;
}
```

>>>

* 結果

![結果](sample4.png)

* [コードサンプル](sample4.html)

---

### その3：テキストのアンダーライン(色付き)

* HTML
```
<div>
    <p>にゃー</p>
</div>
```

>>>

* CSS
```
p {
    position: relative;
}
p::after {
    content: '';
    position: absolute;
    top: calc(100% + 4px);
    left: 0;
    right: 0;
    height: 2px;
    background-color: #0000ff;
}
```

>>>

* 結果

![結果](sample5.png)

* [コードサンプル](sample5.html)

---

### 実際に使用しているサイト

* GC公式・リスティング広告運用代行ページ<br>
  [https://www.glad-cube.com/service/listing.html](https://www.glad-cube.com/service/listing.html)

---

## 使用上の注意
* ::before/::afterではテキストがなくても「content」必須
* HTMLはスッキリするが使いすぎると今度はCSSがカオスに

>>>

### その他(8/5に出た質問)
* 疑似要素のblock/inlineはどうなる？
  * デフォルトではinline
* 疑似要素で使えないstyleはあるか？
  * 明確に「これが出来てこれが出来ない」という資料は見つかっていない
  * アニメーション(animation / transition)については一部ブラウザが非対応。
* 参考：[MDN](https://developer.mozilla.org/ja/docs/Web/CSS/::before) (::before)

---

## まとめ
* 要素の先頭/末尾に付加するものが::before/::after疑似要素
* HTMLだけで書こうとするとカオスになる場合オススメ
* HTMLがスッキリするがCSSがカオスになるので使用時はバランスを考えて
