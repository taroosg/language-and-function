---
transition: "slide"
title: "日本語と関数を活用してプロダクトを実装する"
---

日本語と関数を活用してプロダクトを実装する

<div style="display:flex;justify-content:space-evenly;align-items:center;background:lightgray;">
<img src="https://smarthr.design/static/9eed82f677812bf25862a23e4cf8b60a/6a8a8/%E5%A4%9A%E8%A8%80%E8%AA%9E%E5%8C%96%E5%AF%BE%E5%BF%9C.png" alt="" style="height:120px;">
<img src="https://cdn.pixabay.com/photo/2012/04/11/00/10/math-27248_1280.png" alt="" style="height:100px;">
</div>

---

## 自己紹介

--

|         |                                      |
| ------- | ------------------------------------ |
| Name    | 大杉太郎（たろさん，たろ先生）       |
| Age     | 1987 年生まれ                        |
| Place   | 茨城県 -> 北海道 -> 東京都 -> 福岡県 |
| Career  | 講師，開発（Laravel メイン）         |
| Like1   | Deno，Rust，📚，✈️ 🚃 🚌，🚮         |
| Like2   | 🥃, 🍺, 🍷                           |
| twitter | @taro_osg                            |

--

```txt
                  ＿人人人人人人人人人人人人人人人＿
                  ＞　Deno（Fresh）はいいぞ！！　＜
                  ￣Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y^Y￣
```

---

## もくじ

--

- プロダクトを作るときの流れ

- イメージ

- 細分化する

- コードを書く

- まとめ

---

## プロダクトを作るときの流れ

--

1. 完成図を具体的にイメージする．

2. 処理を細分化し，実装する処理を明確にする．

3. コードを書く．

---

## イメージ

--

全体像をイメージしておく．

イメージできないものは実装できない．

--

- 画面には何が表示されているか．
- 各ボタンをクリックしたら何が起こるのか．
- 全体の目標が達成されるかどうか．

--

（方法は何でも良い）

---

## 細分化する

--

細分化の目的

- やるべきことを整理する．

- 実装の難易度を下げる．

- ググりやすくする．

--

**「細分化」で重要なのは**

**日本語（母国語）の運用能力である．**

--

例

--

HTML・CSS・JavaScript を使ってじゃんけんゲームのプロダクトをつくるぞ！

--

よし，「じゃんけんの処理」をつくろう！！

--

(´・ω・｀;)...??

--

グーチョキパーをそれぞれ 0, 1, 2 で管理するようなルールとし，構造を考えてみる．

--

```txt
じゃんけんをする処理
├── 画面に「グー」「チョキ」「パー」ボタンを表示する
├── ボタンをクリックしたら指定の処理を動かす処理
├── 自分が選択した手を取得する処理
├── 敵の手を定めるためにランダムな数値を発生させる処理
├── 数値をじゃんけんの手に変換する処理
├── 自分の手と敵の手から勝敗を算出する処理
└── 結果を画面に表示する処理
```

--

できるだけ細かくしよう！

--

「入力と出力を明確にする」のがオススメ！

--

```txt
じゃんけんをする処理
├── 画面に「グー」「チョキ」「パー」ボタンを表示する
├── ボタンをクリックしたら指定の処理を動かす処理
├── 自分が選択したボタンの値を取得する処理
├── [✓]最小値と最大値を入力するとその間のランダムな数値を出力する処理
├── [✓]数値を入力するとじゃんけんの手を出力する処理
├── [✓]自分の手（数値）と敵の手（数値）を入力すると勝敗を出力する処理
└── 結果を画面に表示する処理
```

---

## コードを書く

--

コードを書くときは「関数」を活用する．

--

関数を活用することのメリット

- 動作検証がしやすい．

- 各関数はよりシンプルなコードになる．

- 関数を組み合わせた場合でも動作する．

--

**関数のポイント**

**「入力値（引数）」と「出力値（戻り値）」**

--

前項で細分化した文を見ながら式を書けば良い．

--

```js
// 最小値と最大値を入力するとその間のランダムな数値を出力する関数
const generateRandomNumber = (min, max) =>
  ~~(Math.random() * (max - min + 1)) + min;

console.log(generateRandomNumber(0, 2));

// 数値を入力するとじゃんけんの手を出力する関数
const generateJankenHand = (index) => ["グー", "チョキ", "パー"][index];

console.log(generateJankenHand(0));
console.log(generateJankenHand(1));
console.log(generateJankenHand(2));

// プレイヤーの手（数値）と敵の手（数値）を入力すると勝敗を出力する関数
const generateResult = (player_hand_index, computer_hand_index) =>
  [
    ["draw", "win", "lose"],
    ["lose", "draw", "win"],
    ["win", "lose", "draw"],
  ][player_hand_index][computer_hand_index];

console.log(generateResult(0, 1));
console.log(generateResult(1, 1));
console.log(generateResult(2, 0));
```

--

あとは動作検証した関数をまとめて

処理を実装すれば OK．

--

```js
const janken = (e) => {
  // プレイヤーが選択したボタンの値を取得する処理
  const player_hand_index = e.target.value;
  // 最小値と最大値を入力するとその間のランダムな数値を出力する処理
  const computer_hand_index = generateRandomNumber(0, 2);
  // 数値を入力するとじゃんけんの手を出力する処理
  const player_hand = generateJankenHand(player_hand_index);
  const computer_hand = generateJankenHand(computer_hand_index);
  // プレイヤーの手（数値）と敵の手（数値）を入力すると勝敗を出力する処理
  const result = generateResult(player_hand_index, computer_hand_index);
  // 結果を画面に表示する処理
  document.getElementById("player_hand").innerText = player_hand;
  document.getElementById("computer_hand").innerText = computer_hand;
  document.getElementById("result").innerText = result;
};

// ボタンをクリックしたら指定の処理を動かす処理
document
  .getElementById("buttons")
  .addEventListener(
    "click",
    (e) => (e.target.tagName === "BUTTON" ? janken(e) : false),
    true
  );
```

--

全体のコードは以下．

- [https://github.com/taroosg/20230110-lt](https://github.com/taroosg/20230110-lt)

---

## まとめ

--

今回はプロダクトを実装する際の手順を「日本語」「関数」に焦点を当てて解説した．

--

- 全体のイメージをつくれ！

- 処理は「入力値」「出力値」で細分化せよ！

- 各処理を「関数」でつくれ！
