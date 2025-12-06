# Requirements Document

## Introduction
Gerald M. Weinbergの日本語訳書籍（1964年〜2011年、18冊）の一覧を、GitHub Pagesで閲覧可能なシンプルなテーブル形式のシングルページとして構築する。

## Requirements

### Requirement 1: 書籍一覧テーブル
**Objective:** As a 閲覧者, I want 書籍情報をテーブル形式で一覧したい, so that 日本語版と原著の情報を比較・確認できる

#### Acceptance Criteria
1. The Timeline Viewer shall 書籍一覧をHTMLテーブルで表示する
2. The Timeline Viewer shall 各書籍について以下の列を表示する：
   - 日本語版情報：タイトル、著者、出版社、出版年、ISBN
   - 原著情報：原著タイトル、原著出版年、原著出版社
   - 購入リンク：ASIN、Amazonへのリンク
   - 追加情報：著者サイトへのリンク、カテゴリ
3. The Timeline Viewer shall 初期表示時に書籍を日本語版出版年の昇順で表示する
4. If データが存在しない場合, the Timeline Viewer shall 該当セルを「—」で表示する
5. The Timeline Viewer shall ヨミガナをページ上に表示しない（内部データとして保持のみ）

### Requirement 2: テーブルソート機能
**Objective:** As a 閲覧者, I want テーブルを任意の列でソートしたい, so that 目的に応じた順序で書籍を確認できる

#### Acceptance Criteria
1. When 日本語版タイトル列のヘッダーをクリック, the Timeline Viewer shall テーブルをヨミガナでソートする
2. When 原著タイトル列のヘッダーをクリック, the Timeline Viewer shall テーブルを原著タイトルでソートする
3. When 日本語版出版年列のヘッダーをクリック, the Timeline Viewer shall テーブルを日本語版出版年でソートする
4. When 原著出版年列のヘッダーをクリック, the Timeline Viewer shall テーブルを原著出版年でソートする
5. When 同じ列ヘッダーを再度クリック, the Timeline Viewer shall ソート順を昇順/降順で切り替える

### Requirement 3: GitHub Pages対応
**Objective:** As a 管理者, I want GitHub Pagesでホスティングしたい, so that 追加費用なしで公開できる

#### Acceptance Criteria
1. The Timeline Viewer shall 静的ファイル（HTML/CSS/JS）のみで構成される
2. The Timeline Viewer shall GitHub Pagesのデフォルト設定で配信可能である

---

## Data Collection Notes
以下のデータは初期データソース（Gist）に含まれていないため、別途収集が必要：
- ヨミガナ（日本語版タイトルのソート用、非表示）
- 原著タイトル
- 原著出版年
- 原著出版社
- ASIN
- Amazonリンク
- 著者サイトへのリンク
- カテゴリ
