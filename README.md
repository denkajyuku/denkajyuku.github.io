# でんかじゅくLP

## github

[https://github.com/denkajyuku/denkajyuku.github.io.git](https://github.com/denkajyuku/denkajyuku.github.io.git)

## 公開URL

[https://denkajyuku.github.io](https://denkajyuku.github.io)

## 開発環境

parcelを使用して開発環境の設定を短縮。github pagesを使用しているのでリポジトリのマスターブランチがそのまま公開されます。

### 環境のセットアップ

```
$ npm ci
```

### 開発環境の立ち上げ

```
$ npm start
```

以下にアクセスして確認できます。

[http://localhost:1234](http://localhost:1234)

### 使用可能

- pug
- scss
- javascript(ES6)

### ディレクトリ構造

```
root
 + .cache
 + node_modules
 + src
 - + js
 - - + modules
 - - - - module.js
 - - - script.js
 - + css
 - - - style.css
 - .gitignore
 - .postcssrc
 - index.html
 - package-lock.json
 - package.json
 - README.md
 - script.*.js
 - script.*.js.map
 - style.*.css
 - style.*.css.map
 - style.*.js
 - style.*.js.map
```

***
## CSS設計

### CSS設計 - FLOUの独自拡張
ディレクトリ構造
```
root
  └── src
       └── css
           ├── foundation
           │     │
           │     ├── _animation.scss
           │     ├── _base.scss
           │     ├── _colors.scss
           │     ├── _fonts.scss
           │     ├── _functions.scss
           │     ├── _mixins.scss
           │     ├── _reset.scss
           │     └── _variables.scss
           │
           ├── layout
           │     ├── _footer.scss
           │     ├── _header.scss
           │     ├── _heading.scss
           │     └── _section.scss
           │
           ├── sections
           │     └── _section○○.scss
           │
           └── style.scss
```

#### foundation層
土台を作る階層(基本的に触らない)
<dl>
  <dt>_animation.scss</dt>
  <dd>Keyframeの設定</dd>
  <dt>_colors.scss</dt>
  <dd>色をmapで管理する</dd>
  <dt>_fonts.scss</dt>
  <dd>フォントの設定</dd>
  <dt>_variables.scss</dt>
  <dd>メディアクエリー、zindexの管理</dd>
</dl>

#### layout層
**サイト共通**のレイアウトを作る層  
今後共通パーツがある場合は増やして良い

#### sections層(今回特注)
今回はsection毎に別れて作業してもらうので各section中の内容コードはここに集約する

### CSS命名規則 - MindBEMdingの独自拡張
**ローカルルール(強制ではないが推奨)**
1. Blockは1単語または、2単語(2単語の場合ダッシュで区切る)。
```html
<!-- NG -->
<div class="hoge-huga-piyo"><div>
<div class="hoge_huga"><div>
<div class="hogeHuga"><div>
```
2. Elementは1単語。
```html
<!-- NG -->
<div class="block__hoge-huga"><div>
<div class="block__hoge_huga"><div>
<div class="block__hogeHuga"><div>
```
3. Elementの中にmodifire以外をネストするのはNG。
```html
<!-- NG -->
<div class="block__element__block"><div>
<div class="block__element__element"><div>
```
4. 一時的な状態を示すステートはSMACSSのis-hoge~~または、aria属性~~で管理する。
```html
<!-- OK -->
<div class="block__element is-active"><div>
<div class="block__element is-show"><div>
```
5. BEMのmodifireは冗長なのでRSCSSの-hogeにする。
```html
<!-- OK -->
<div class="block__element -small"><div>
<div class="block__element -red"><div>
```
6. 詳細度が高いためIDセレクタの使用は禁止。
6. 極力タグセレクタを避ける。
```scss
.hoge {
  //NG
  > h2 {
    //これは修正の時にh2では無くなる可能性もあるのでなるべく避ける
  }
  //非推奨
  &__list > li {
    //ulの直下はliのみだがこれもなるべく避けた方が良い
  }
  &__huga {
    > a {
      //aタグは詳細度が負ける事があるのでギリギリセーフ
    }
  }
  //※このパータンも可
  $this: &;
  &__huga {
    #{$this}__link {
    }
  }
}
```
### サンプルコード
coming soon...

<!--
```html
<section class="hoge">
  <h1 class="hoge__title">タイトル1</h1>
  <p class="hoge__text">テキスト1</p>
  <ul class="hoge__list">
    <li class="hoge__item">
      <section class="hoge-card is-new">
        <h2 class="hoge-card__title">タイトル2</h2>
        <p class="hoge-card__text">テキスト2</p>
        <a class="hoge-card__link" href="/" aria-label="○○についての続きを読む">続きを読む</a>
        <div class="hoge-card__img"><img src="/sample.png" alt=""></div>
      </section>
    </li>
    <li class="hoge__item">
      <section class="hoge-card">
        <h2 class="hoge-card__title -small">タイトル2</h2>
        <p class="hoge-card__text">テキスト2</p>
        <a class="hoge-card__link" href="/" aria-label="○○についての続きを読む">続きを読む</a>
        <div class="hoge-card__img"><img src="/sample.png" alt=""></div>
      </section>
    </li>
    <li class="hoge__item">
      <section class="hoge-card">
        <h2 class="hoge-card__title">タイトル2</h2>
        <p class="hoge-card__text">テキスト2</p>
        <a class="hoge-card__link" href="/" aria-label="○○についての続きを読む">続きを読む</a>
        <div class="hoge-card__img"><img src="/sample.png" alt=""></div>
      </section>
    </li>
  </ul>
</section>
```

```scss
.hoge {
  $this: &;
  &__title {

  }
  &__text {

  }
  &__list {

  }
  &__item {

  }
}

.hoge-card {
  $this: &;
  &__title {

  }
  &__text {
  }
  &__link {
  }
  &__img {
    > img {

    }
  }
}
``` -->