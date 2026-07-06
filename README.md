# Museum Quest v0.2

展示・作品・場所を「QUEST」として巡る、軽量なブラウザ型ミュージアム体験テンプレートです。

HTML 1ファイルで動作し、サーバーやデータベースは不要です。
GitHub Pages などの静的ホスティングで公開できます。

## 主な機能

- 複数QUESTの表示
- 選択式クイズ
- 正解時のメッセージ表示
- QUESTクリア進捗の保存
- 一定数クリア後のENDING解放
- 感想フォームへの外部リンク
- テスト用進捗リセット
- 設定値の簡易バリデーション
- JavaScript無効時の案内

## 使い方

基本的に編集するのは、HTML内の次の設定部分です。

```js
const EXPERIENCE = {
  // ここを編集
};
```

## 基本設定

```js
title: "消えた火の記憶",
intro: "縄文の展示室に、三つの記憶が眠っている。",
unlockEndingAt: 3,
feedbackUrl: "https://example.com/form",
```

- `title`：体験全体のタイトル
- `intro`：最初に表示する導入文
- `unlockEndingAt`：何問クリアでENDINGを解放するか
- `feedbackUrl`：Googleフォームなどの感想フォームURL

## ENDING設定

```js
ending: {
  title: "火は、誰のものだったのか",
  text: "三つの記憶がつながった。"
}
```

## QUEST設定

```js
{
  id: "q1",
  title: "炎のかたち",
  story: "夜の集落から火が消えた。",
  question: "展示された土器を見よ。最も目立つ装飾はどこに集中している？",
  choices: ["底の近く", "口縁部の近く", "内側だけ"],
  correct: 1,
  success: "記憶が反応した。"
}
```

## correct の注意

`correct` は 0 から数えます。

```js
choices: ["A", "B", "C"],
correct: 0
```

この場合、正解は `A` です。

```js
correct: 1
```

なら `B` が正解です。

## QUESTを追加する

既存のQUESTオブジェクトを複製し、`quests` 配列内に追加します。

```js
{
  id: "q4",
  title: "新しい記憶",
  story: "ここに導入文",
  question: "ここに質問文",
  choices: [
    "選択肢A",
    "選択肢B",
    "選択肢C"
  ],
  correct: 0,
  success: "正解時のメッセージ"
}
```

`id` はQUESTごとに重複しない値を設定してください。

## ENDING解放条件

`unlockEndingAt` の値で、ENDING解放に必要なQUESTクリア数を変更できます。

```js
unlockEndingAt: 3
```

たとえば `2` にすると、2つのQUESTをクリアした時点でENDINGが解放されます。

## 感想フォーム

`feedbackUrl` にGoogleフォームなどのURLを設定します。

```js
feedbackUrl: "https://example.com/form"
```

空文字の場合は、感想フォームへの導線を使用しない構成として扱ってください。

## 進捗保存

QUESTのクリア進捗はブラウザ側に保存されます。
同じブラウザ・同じ保存領域では、ページを再読み込みしても進捗が残ります。

## テスト用リセット

「テスト用：進捗をリセット」ボタンで保存済み進捗を削除できます。
公開運用時は、必要に応じてこのボタンを非表示または削除してください。

## 公開方法

静的HTMLとして公開できます。

例：

- GitHub Pages
- Netlify
- Cloudflare Pages
- 一般的なWebサーバー

## ファイル構成

最小構成ではHTML 1ファイルだけで動作します。

```text
index.html
```

## 注意事項

- QUESTの`id`は重複させないでください
- `correct`は0始まりです
- `unlockEndingAt`はQUEST数との整合性を確認してください
- 外部フォームURLは公開前に動作確認してください
- 本番公開前にスマートフォン表示を確認してください

## ライセンス

ライセンス方針は配布・販売形態に合わせて設定してください。
