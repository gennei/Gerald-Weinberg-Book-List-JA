# Research & Design Decisions

## Summary
- **Feature**: `weinberg-timeline-viewer`
- **Discovery Scope**: New Feature (Simple Addition)
- **Key Findings**:
  - 静的HTML/CSS/JSのみでソート可能なテーブルを実装可能
  - 外部ライブラリなしでVanilla JSによるソート実装が最適
  - JSONファイルでデータ管理することで更新容易性を確保

## Research Log

### テーブルソート実装アプローチ
- **Context**: 4列でソート可能なテーブルをGitHub Pages上で動作させる必要がある
- **Sources Consulted**:
  - MDN Web Docs: Array.prototype.sort()
  - 一般的なテーブルソートライブラリ（list.js, tablesort, DataTables）
- **Findings**:
  - 18行程度の小規模データであれば、Vanilla JSで十分対応可能
  - 外部ライブラリは依存関係管理のオーバーヘッドが発生
  - localeCompare()で日本語ソートも適切に処理可能
- **Implications**: 外部依存なしのVanilla JS実装を採用

### データ管理形式
- **Context**: 書籍データの更新容易性とページ表示の両立
- **Sources Consulted**: GitHub Pages静的サイト構成パターン
- **Findings**:
  - 別ファイルのJSONをfetchで読み込む方式が更新しやすい
  - HTMLに埋め込む方式は単一ファイルだが更新時の編集範囲が広い
  - JSON形式なら構造化されており、将来的な拡張も容易
- **Implications**: 外部JSONファイル方式を採用

### ヨミガナソートの実装
- **Context**: 日本語タイトルをヨミガナでソートし、ヨミガナ自体は非表示
- **Sources Consulted**: HTML data属性の活用パターン
- **Findings**:
  - data-sort-key属性にヨミガナを格納し、ソート時のみ参照する方式が一般的
  - JSONデータ内にyomiganaフィールドを持ち、DOMには反映しない
- **Implications**: JSONにyomiganaフィールドを持ち、ソート処理でのみ使用

## Architecture Pattern Evaluation

| Option | Description | Strengths | Risks / Limitations | Notes |
|--------|-------------|-----------|---------------------|-------|
| Single HTML + Embedded Data | 全てを1ファイルに含む | デプロイが簡単 | データ更新時にHTML編集が必要 | 却下 |
| HTML + External JSON | データを別ファイル管理 | データ更新が容易、関心の分離 | fetchが必要（ローカル開発時にCORS注意） | 採用 |
| Static Site Generator | Jekyll等でビルド | テンプレート活用可能 | オーバーエンジニアリング | 却下 |

## Design Decisions

### Decision: Vanilla JavaScript によるソート実装
- **Context**: ソート機能をGitHub Pages上で動作させる
- **Alternatives Considered**:
  1. Vanilla JavaScript — 依存なし、軽量
  2. list.js — 軽量ライブラリ、検索機能も付属
  3. DataTables — 高機能、jQueryに依存
- **Selected Approach**: Vanilla JavaScript
- **Rationale**: 18行の小規模データに対してライブラリは過剰。シンプルさと依存ゼロを優先
- **Trade-offs**: 自前実装のため若干のコード量増加、ただし理解・保守が容易
- **Follow-up**: ソートロジックの単体テストを検討

### Decision: 外部JSONファイルによるデータ管理
- **Context**: 書籍データを管理者が容易に更新できる必要がある
- **Selected Approach**: `data/books.json`として分離
- **Rationale**: JSONファイルのみ編集すればデータ更新完了。HTMLロジックに影響なし
- **Trade-offs**: ローカル開発時はローカルサーバーが必要（file://でのfetchはCORSエラー）

## Risks & Mitigations
- **リスク1**: ローカル開発時のCORSエラー → Python等の簡易サーバーで対応、またはLive Server拡張
- **リスク2**: 追加収集データの欠損 → 欠損時は「—」表示で対応（要件1.4）
- **リスク3**: 著者サイトURLの有効性 → リンク切れの可能性があるが、静的サイトのため定期確認で対応

## References
- [MDN: Array.prototype.sort()](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
- [MDN: String.prototype.localeCompare()](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare)
- [GitHub Pages Documentation](https://docs.github.com/ja/pages)
