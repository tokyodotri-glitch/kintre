# 鍛錬 / Kintore — Training Log

iPhone のホーム画面から起動できる、シンプルなフリーウェイト・トレーニング記録アプリ。
バックエンド不要、依存パッケージなし、`index.html` 1ファイルで完結します。

![tab](https://img.shields.io/badge/tabs-記録%20|%20履歴%20|%20推移%20|%20連携-d4ff00?style=flat-square&labelColor=0a0a0a)
![storage](https://img.shields.io/badge/storage-localStorage-888?style=flat-square&labelColor=0a0a0a)
![license](https://img.shields.io/badge/license-MIT-888?style=flat-square&labelColor=0a0a0a)

---

## 機能

- **記録** — 部位別ピッカー（胸 / 背 / 肩 / 腕 / 脚 / 体幹 / カスタム）から種目を選択し、セット × 重量 × レップを入力
- **履歴** — セッション別に展開可能。総ボリューム・部位コード表示
- **推移** — 種目別の折れ線グラフ。最大重量 / 総ボリューム / 推定1RM (Epley式) を切替
- **連携**
  - Notion 用 Markdown をクリップボードにコピー
  - Google カレンダー用 `.ics` をダウンロード
  - 全データを JSON でバックアップ / 復元

依存ゼロ。React も Babel も外部CDNも使っていません。`index.html` 1ファイルだけ。

---

## iPhone へのインストール (PWA 化)

1. このリポジトリで GitHub Pages を有効化（下記参照）
2. 発行された URL を iPhone の **Safari** で開く
3. 共有ボタン → **「ホーム画面に追加」**
4. ホーム画面のアイコンをタップするとフルスクリーンで起動

データは Safari の `localStorage` に保存されます。Safari のサイトデータを消すと記録も消えるため、定期的に「連携」タブから JSON バックアップを取ってください。

---

## GitHub にアップする手順

### A. ブラウザだけで完結する方法（推奨・最速）

1. GitHub にログインし、右上の **+ → New repository** をクリック
2. Repository name に `kintore`（任意）を入力、**Public** を選択、**Add a README file** にチェック → **Create repository**
3. 作成されたリポジトリのページで **Add file → Upload files**
4. 手元の `index.html` と `README.md` をドラッグ＆ドロップ → **Commit changes**

### B. コマンドラインから

```bash
# 新しいフォルダで初期化
mkdir kintore && cd kintore

# index.html と README.md を配置（このリポジトリの内容をコピー）

git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<YOUR_USERNAME>/kintore.git
git push -u origin main
```

---

## GitHub Pages で公開する

1. リポジトリの **Settings → Pages**
2. **Source** で `Deploy from a branch` を選択
3. **Branch** を `main` / `(root)` に設定 → **Save**
4. 数十秒後にページ上部に `https://<YOUR_USERNAME>.github.io/kintore/` のような URL が表示される
5. その URL を iPhone の Safari で開く

---

## ファイル構成

```
kintore/
├── index.html      ← アプリ本体（React + Recharts を CDN から読み込み）
├── README.md
└── .gitignore
```

ビルドステップなし。`index.html` を直接ブラウザで開けば動きます。

---

## 技術メモ

- 依存ライブラリなし（Vanilla JavaScript + SVG）
- データ永続化は `localStorage`（端末ローカル）
- 推定1RMは Epley 式 `weight × (1 + reps / 30)`
- ストリーク日数はトップ右上に表示（連続記録日カウンタ）
- ファイル1個・約42KB。オフラインでも動作

---

## カスタマイズしたい場合

`index.html` 内の `EXERCISE_LIBRARY` を編集すると種目リストを変更できます。
配色は `const C = { ... }` でまとめて管理しています。

---

## ライセンス

MIT
