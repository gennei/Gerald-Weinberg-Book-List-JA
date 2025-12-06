# Gerald M. Weinberg 日本語訳書籍一覧

Gerald M. Weinberg（ジェラルド・ワインバーグ）の日本語訳書籍情報をまとめています。

## 機能

- 書籍一覧のテーブル表示
- 4つのカラムでソート可能
  - タイトル（読み仮名順）
  - 出版年
  - 原著タイトル
  - 原著出版年
- Amazon.co.jpへのリンク（ASIN経由）
- 著者公式サイトへのリンク（原著タイトル経由）
- カラム幅のドラッグ調整

## 表示項目

| 和書情報 | 原著情報 |
|----------|----------|
| タイトル | 原著タイトル |
| 著者・訳者 | — |
| 出版年 | 原著出版年 |
| 出版社 | 原著出版社 |
| ISBN | — |
| — | ASIN(JP) |
| — | カテゴリ |

## 使い方

### ローカルでの確認

```bash
# 任意のHTTPサーバーで配信
python3 -m http.server 8080
```

ブラウザで `http://localhost:8080` を開きます。

## ディレクトリ構成

```
.
├── index.html          # メインHTML
├── css/
│   └── styles.css      # スタイルシート
├── js/
│   └── main.js         # アプリケーションロジック
└── data/
    └── books.json      # 書籍データ
```

## データソース

- 日本語書籍情報: [国立国会図書館サーチ](https://ndlsearch.ndl.go.jp/)
- 原著情報・カテゴリ: [Gerald M. Weinberg 公式サイト](https://geraldmweinberg.com/)
- Amazon情報: [Amazon.co.jp](https://www.amazon.co.jp/)

## 貢献

書籍情報の追加・修正のご提案は、Issue または Pull Request にてお待ちしています。

## ライセンス

MIT License
