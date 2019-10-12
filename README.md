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
 - .cache
 - node_modules
 - src
 .gitignore
 .postcssrc
 index.html
 package-lock.json
 package.json
 README.md
 script.*.js
 script.*.js.map
 style.*.css
 style.*.css.map
 style.*.js
 style.*.js.map
```
