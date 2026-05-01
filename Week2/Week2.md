# Week ２: Webの基本とフロントエンド実装

<aside>
💡

- **内容**:
    - Webの基本（フロントエンド、バックエンド、APIの関係）。
    - HTML, CSS, JavaScriptで「動的なチャットUI」を作成。
- **成果物**: メッセージ入力と表示ができる「シンプルなチャットUI」。

</aside>

![sayhello.png](/Users/taichikondo/everyonesWebDevelopment/Week2/Week2/sayhello.png)

Week1で見たこの３つを更に詳しく見ていきます。

その前に、Web開発に必要な「ディレクトリ構成」という概念をご説明します。

シンプルなWebアプリでは、以下のような構成を取るのが一般的です。

```
project-root/
│── frontend/         # フロントエンド関連のコード
│   ├── index.html    # メインのHTMLファイル
│   ├── styles.css    # スタイル（デザイン）を記述するファイル
│   ├── script.js     # JavaScriptの処理を記述するファイル
│   ├── assets/       # 画像やアイコンなどを保存
│   ├── components/   # UIの部品（Reactの場合など）
│── backend/          # バックエンド関連のコード
│   ├── server.js     # APIを提供するサーバー
│   ├── routes/       # APIのルーティングを管理
│   ├── models/       # データモデル（データベース関連）
│── README.md         # プロジェクトの説明書
│── .gitignore        # Gitで管理しないファイルを指定

```

---

一つのプロジェクトの配下に、いくつものフォルダとファイルを用意します。

また、プロジェクトの下にいくつものフォルダを用意することで、どの機能をどこに用意しているかを把握できるので、いくつかフォルダを用意して、その下で必要なファイルを作成します。

ちなみにこの界隈ではフォルダのことを「ディレクトリ」と呼びます。両者は全く同じ意味なので、ディレクトリといったほうがかっこいいのでこちらの表現を使うようにしましょう。例えば「カレントディレクトリ」と言われれば、今自分がいるフォルダのことを指します。

## HTMLとは？

**📌 HTML（エイチティーエムエル）とは？**

前回見たかと思いますが確認です。

HTML（HyperText Markup Language）は、**Webページの骨組み（構造）**を作るための言語です。

例えば、Webページに「見出し」「文章」「画像」「ボタン」などを配置するために使います。

```html
<!DOCTYPE html>
<html>
<head>
    <title>私のページ</title>
</head>
<body>
    <h1>こんにちは！</h1>
    <p>これはHTMLで作ったWebページです。</p>
</body>
</html>
```

上のコードでは下記の画面が表示されます。

VSコードで上のコードを貼り付けてGo Liveをクリックしてください（詳しくはWeek1参照）

![image.png](Week%20%EF%BC%92%20Web%E3%81%AE%E5%9F%BA%E6%9C%AC%E3%81%A8%E3%83%95%E3%83%AD%E3%83%B3%E3%83%88%E3%82%A8%E3%83%B3%E3%83%89%E5%AE%9F%E8%A3%85/image%201.png)

htmlでは<xxx></xxx>の形（タグ）を使うことでwebページの構造を作ります。

タグを正しく書くことでいろいろなページを表現できます。

### HTMLのルール

- **開始タグ `<タグ>` と終了タグ `</タグ>` で囲む**
    - 例：`<p>これは段落です。</p>`
    - 例外：`<img>` や `<br>` は単独で使える（閉じタグなし）
- **タグの中に「属性」を書ける**
    - `属性 = "値"` の形で追加できる
    - 例：`<a href="https://example.com">リンク</a>`
    → `href="URL"` でリンク先を指定
- **ネスト（入れ子）にできる**
    - `<div>` などを使ってグループ化できる

### **よく使うHTMLタグ一覧**

| **タグ** | **意味** | **例** |
| --- | --- | --- |
| `<h1>～<h6>` | 見出し（大きさ1～6） | `<h1>大見出し</h1>` |
| `<p>` | 段落（文章） | `<p>これは文章です。</p>` |
| `<a>` | リンク | `<a href="https://example.com">こちら</a>`
とすることで「こちら」にhttps://example.comのURLが作成されます。 |
| `<img>` | 画像 | `<img src="image.jpg" alt="説明">` |
| `<ul>` | 箇条書きリスト | `<ul><li>項目1</li><li>項目2</li></ul>` |
| `<ol>` | 番号付きリスト | `<ol><li>1つ目</li><li>2つ目</li></ol>` |
| `<table>` | 表（テーブル） | `<table><tr><td>データ</td></tr></table>` |
| `<button>` | ボタン | `<button>クリック！</button>` とするとボタンができます。 |

これらを全て使ったhtmlのコードを以下のページに作りました。よければコピペしてindex.htmlというファイルを作り、Go Liveしてください

[htmlのコード](https://www.notion.so/html-1bc0cc9f5af380dbb40df0405511f170?pvs=21)

ちなみにChromeだと⌘+option+I　で「デベロッパーツール」というのが開き、そのwebページのHTML情報を閲覧できます。

ちょこちょこいじいじしてみてもいいかもしれません。

## CSSとは？

お分かりの通り、htmlだけで作ったページは、白と黒のシンプルな何の面白みもないページになります。

流石に色とかつけたいよなあと思うと思うので、そのようなときに使えるのがCSS（Cascading Style Sheets）です。

CSSはHTMLの補完的な存在で、HTMLで作成したタグ（要素）に対して、**どのような見た目（デザイン）にするかの情報を与えるもの**です。

たとえば、文字の色やサイズ、背景色、レイアウトなどを指定できます。

before

![image.png](Week%20%EF%BC%92%20Web%E3%81%AE%E5%9F%BA%E6%9C%AC%E3%81%A8%E3%83%95%E3%83%AD%E3%83%B3%E3%83%88%E3%82%A8%E3%83%B3%E3%83%89%E5%AE%9F%E8%A3%85/image%201.png)

after

![image.png](Week%20%EF%BC%92%20Web%E3%81%AE%E5%9F%BA%E6%9C%AC%E3%81%A8%E3%83%95%E3%83%AD%E3%83%B3%E3%83%88%E3%82%A8%E3%83%B3%E3%83%89%E5%AE%9F%E8%A3%85/image%202.png)

cssを適用するためにはhtmlの中でどのcssを参照するか？というコードを含める必要があり、若干変更が必要です。

以下のhtml cssのコードをそれぞれVSコードでファイルを分けて作り、Go Liveして動作確認してください。

HTML（ファイル名index.html）

```html
<!DOCTYPE html>
<html>
<head>
    <title>私のページ</title>
    <link rel="stylesheet" href="style.css">  <!-- CSSを読み込む -->
</head>
<body>
    <h1>こんにちは！</h1>
    <p>これはHTMLで作ったWebページです。</p>
</body>
</html>

```

CSS（ファイル名style.css）

```css
/* ページ全体の背景と文字設定 */
body {
    background-color: #f0f8ff;  /* 明るい水色の背景 */
    font-family: 'Arial', sans-serif;
    color: #333;
    margin: 0;
    padding: 40px;
    text-align: center;
}

/* h1 見出しのスタイル */
h1 {
    color: #ff6b6b;            /* 明るい赤系の文字色 */
    font-size: 36px;
    margin-bottom: 10px;
}

/* p 段落のスタイル */
p {
    font-size: 18px;
    line-height: 1.6;
    color: #555;
}

```

[Screen Recording 2025-03-21 at 17.55.51.mov](Week%20%EF%BC%92%20Web%E3%81%AE%E5%9F%BA%E6%9C%AC%E3%81%A8%E3%83%95%E3%83%AD%E3%83%B3%E3%83%88%E3%82%A8%E3%83%B3%E3%83%89%E5%AE%9F%E8%A3%85/Screen_Recording_2025-03-21_at_17.55.51.mov)

cssのコードでは、

```css
セレクタ {
プロパティ: 値;
プロパティ: 値;
}
```

の形式で記述します。セレクタというのは、どのHTMLタグに対してデザインを適用するかを指定するところで、<p>に対してならp <kondo>に対してならkondoと記述します。

プロパティは色（color）やフォント（font）などの項目を指定する部分で、自分のやりたいフォントや色を設定して値のところに記述します。

冒頭に述べたように、「色などをつけた見やすいwebページを作る」というタスクだけで、２つのファイルを使う必要があります。

複数のファイルをいじいじすることで全てのアプリケーションは動作します。ディレクトリ構成をしっかり考えましょう。

### Q：問題

CSSの

```
/* p 段落のスタイル */
p {
    font-size: 18px;
    line-height: 1.6;
    color: #555;
}
```

を

```
/* p 段落のスタイル */
p {
font-size: 2px;
line-height: 1.6;
color: #555;
}
```

にすると、どの部分がどうなりますか？？

### A: 答え

- この中を開く
    
    「これはHTMLで作ったWebページです。」のフォントが2pxになる。
    

## JavaScriptとは？

HTMLとCSSは「静的なページ」を作る上では十分なのですが、「動的なページ」を作る上では不十分な言語です。

「動的なページ」というのは、**ユーザーの操作や外部の情報に応じて内容が変わるページ**のことを指します。

例えば、、

- ユーザーが入力した名前を画面に表示するページ
- 天気予報サイトやニュースサイトのように、毎回アクセスしたときに違う情報が表示されるページ
- チャットアプリのように、送信ボタンを押すと会話が画面に追加されるページ
- ネットショッピングのように、ボタンを押すとカートに商品が追加されるページ

が挙げられます。

JavaScriptを用いることで、そのような変化にも柔軟なwebページを作ることができます。

では以下の3つのコードをそれぞれindex.html styles.css script.jsというファイル名にしてコピペしてみてください

index.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>私のページ</title>
    <link rel="stylesheet" href="style.css">  <!-- CSSを読み込む -->
</head>
<body>    
    <button id="changeTextBtn">メッセージを変更</button>
    <p id="dynamicText">これはHTMLで作ったWebページです。</p>

    <script src="script.js"></script>  <!-- JavaScriptを読み込む -->
</body>
</html>
```

style.css

```css
/* ページ全体の背景と文字設定 */
body {
    background-color: #f0f8ff;  /* 明るい水色の背景 */
    font-family: 'Arial', sans-serif;
    color: #333;
    margin: 0;
    padding: 40px;
    text-align: center;
}

/* h1 見出しのスタイル */
h1 {
    color: #ff6b6b;            /* 明るい赤系の文字色 */
    font-size: 36px;
    margin-bottom: 10px;
}

/* p 段落のスタイル */
p {
    font-size: 18px;
    line-height: 1.6;
    color: #555;
}

/* ボタンのスタイル */
button {
    padding: 10px 20px;
    font-size: 16px;
    background-color: #4caf50;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    margin-top: 20px;
}

button:hover {
    background-color: #45a049;
}

```

script.js

```jsx
document.getElementById("changeTextBtn").addEventListener("click", function() {
    const textElement = document.getElementById("dynamicText");
    textElement.textContent = "ボタンがクリックされました！";
});

```

[Screen Recording 2025-03-22 at 1.47.56.mov](Week%20%EF%BC%92%20Web%E3%81%AE%E5%9F%BA%E6%9C%AC%E3%81%A8%E3%83%95%E3%83%AD%E3%83%B3%E3%83%88%E3%82%A8%E3%83%B3%E3%83%89%E5%AE%9F%E8%A3%85/Screen_Recording_2025-03-22_at_1.47.56.mov)

ボタンを押すと画面が変わることがわかります。これがJavaScriptの凄さです

ちなみにJavaというプログラミング言語がありますが、こちらは全く似て非なる存在です。例えるならグレープとグレープフルーツ、テニスとテーブルテニスみたいな違いです。

いくつか主要なJavaScriptの関数を理解しておきましょう。適宜ページ配下にある動画を参照してください。

### 🟢 1. `alert()`

💬 **画面にポップアップを表示してメッセージを伝える関数**です。

```jsx
alert("こんにちは！");
```

👉 ブラウザ上に「こんにちは！」というポップアップが表示されます。初心者の練習にピッタリです！

[動画](https://www.notion.so/1be0cc9f5af3806fb2bddcc8d9af86b2?pvs=21)

---

### 🟢 2. `console.log()`

💬 **開発中に値を確認するための「ログ出力」関数**です。コンソール（開発者ツール）に表示されます。

このデベロッパーツールはHTMLのときの紹介したwebページの構成を見れるツールです。

web開発を行う上で非常によく利用するツールなので、使い方に慣れましょう。

下記を実行することで、画面ではなく、デベロッパーツールのlog上に出力されます

```jsx
console.log("これはテストメッセージです")
```

👉 デバッグ時にとても便利。何が起きているか確認できます。

[動画](https://www.notion.so/1be0cc9f5af3802f89b3c94615de87e8?pvs=21)

---

### 🟢 3. `prompt()`

💬 **ユーザーからの入力を受け取る関数**です。

```jsx
const name = prompt("あなたの名前は？");
alert(`こんにちは、${name}さん！`)
```

👉 入力した名前が`name`という変数に保存され、それを使って挨拶できます。

[動画](https://www.notion.so/1be0cc9f5af380c7a64fdf8458ca8f9a?pvs=21)

---

### 🟢 4. `parseInt()` / `parseFloat()`

💬 **文字列を数字に変換する関数**です。

```jsx
const input = prompt("年齢を入力してください");
const age = parseInt(input);
console.log(age + 1); // 来年の年齢を表示
```

👉 `parseInt()` は整数、`parseFloat()` は小数を扱えます。

[動画](https://www.notion.so/1be0cc9f5af380a89cc5f2cdd252c9f5?pvs=21)

---

### 🟢 5. `setTimeout()`

💬 **指定した時間後に何かを実行する関数**です。

```jsx
setTimeout(() => {
  alert("3秒後に表示されます！");
}, 3000); // 3000ミリ秒（＝3秒）
```

👉 時間を指定して「後で動く処理」を書くことができます。

[動画](https://www.notion.so/1be0cc9f5af380d7aa30c6324454b204?pvs=21)

---

### 🟢 6. `addEventListener()`

💬 **ボタンなどに「クリックしたときの処理」を追加する関数**です。

htmlとともに修正してみましょう。

```html
<!DOCTYPE html>
<html>
<head>
    <title>私のページ</title>
</head>
<body>    
  <button id="btn">押してみて！</button>
    <p id="dynamicText">これはHTMLで作ったWebページです。</p>

    <script src="script.js"></script>  <!-- JavaScriptを読み込む -->
</body>
</html>
```

```jsx
document.getElementById("btn").addEventListener("click", () => {
  alert("ボタンが押されました！");
});
```

👉 Webページを「動かす」ための超基本です。

[動画](https://www.notion.so/1be0cc9f5af3806b93d0c807965e02a6?pvs=21)

# 演習１：自分GPT（大嘘）を作ろう！（コピペ形式）

## 1.以下の内容をコピペしてください。

index.html

style.css

script.js

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>???ボット</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <h1>???ボット</h1>
  <div id="chat"></div>
  <input type="text" id="userInput" placeholder="質問を入力..." />
  <button onclick="handleQuestion()">送信</button>

  <script src="script.js"></script>
</body>
</html>

```

```css
body {
  font-family: Arial, sans-serif;
  max-width: 600px;
  margin: 40px auto;
  padding: 20px;
  background-color: #f0f8ff;
  border-radius: 10px;
}

#chat {
  height: 300px;
  overflow-y: auto;
  border: 1px solid #ccc;
  padding: 10px;
  background-color: #fff;
  margin-bottom: 10px;
  border-radius: 5px;
}

.message {
  margin-bottom: 10px;
}

.user {
  text-align: right;
  color: blue;
}

.bot {
  text-align: left;
  color: green;
}

```

```css
const chat = document.getElementById("chat");
const userInput = document.getElementById("userInput");

function handleQuestion() {
  const question = userInput.value.trim();
  if (!question) return;

  addMessage(question, "user");
  const answer = getAnswer(question);
  addMessage(answer, "bot");
  userInput.value = "";
}

function addMessage(text, sender) {
  const message = document.createElement("div");
  message.className = "message " + sender;
  message.innerText = text;
  chat.appendChild(message);
  chat.scrollTop = chat.scrollHeight;
}

function getAnswer(question) {
  if (question.includes("名前")) {
    return "私は???です。";
  } else if (question.includes("趣味")) {
    return "???です。";
  } else if (question.includes("出身")) {
    return "???です！";
  } else {
    return "ごめんなさい、よくわかりません。";
  }
}

```

## 2.空欄（???）を埋めよう。やりたければ質問の項目を増やしても良い

近藤の場合（誰得）

```css
const chat = document.getElementById("chat");
const userInput = document.getElementById("userInput");

function handleQuestion() {
  const question = userInput.value.trim();
  if (!question) return;

  addMessage(question, "user");
  const answer = getAnswer(question);
  addMessage(answer, "bot");
  userInput.value = "";
}

function addMessage(text, sender) {
  const message = document.createElement("div");
  message.className = "message " + sender;
  message.innerText = text;
  chat.appendChild(message);
  chat.scrollTop = chat.scrollHeight;
}

function getAnswer(question) {
  if (question.includes("名前")) {
    return "私は近藤汰一です。";
  } else if (question.includes("趣味")) {
    return "空手です。";
  } else if (question.includes("出身")) {
    return "神戸です！";
  } else {
    return "ごめんなさい、よくわかりません。";
  }
}

```

[動画](https://www.notion.so/1be0cc9f5af380c98213f8b6d732523a?pvs=21)

## 3. 隣の人と質問のやりとりをしてみよう！

いろいろな質問を試してみよう！もしかしたら出身、名前、趣味以外に何か質問が用意されているかも？？？

## 4. 以下の流れでgithubにプッシュしてみよう。そして他の人がクローンして自分の手元でその人について知ろう！

プッシュの流れ

[Screen Recording 2025-05-07 at 17.44.03.mov](Week%20%EF%BC%92%20Web%E3%81%AE%E5%9F%BA%E6%9C%AC%E3%81%A8%E3%83%95%E3%83%AD%E3%83%B3%E3%83%88%E3%82%A8%E3%83%B3%E3%83%89%E5%AE%9F%E8%A3%85/Screen_Recording_2025-05-07_at_17.44.03.mov)

# 演習２：自分GPTのUIを変更しよう！（バイブコーディング）

以下のプロンプトをChatGPT（などの生成AI）に打ち込み、その結果をコピペしてみましょう。？？は自分なりに変えてください。またプロンプトも自由に変えてもらってOKです。

```
index.html style.css script.jsの３つのファイルを使って、
自分に関する情報のリクエストが届いたら内容を返す自分GPTを作ろう。
「？？」と聞かれたら「？？」、
「？？」と聞かれたら「？？」、
「？？」と聞かれたら「？？」と返すようにして、それ以外が入力されれば「答えられない」と返して

UIは？？を意識して、フロントエンドだけで動くサービスにしてほしい
```

できたらpushしてみましょう。やり方は先程のものを参照してください。