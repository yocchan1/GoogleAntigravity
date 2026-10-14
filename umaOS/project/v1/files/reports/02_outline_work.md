# 大枠指示書 (02_outline_work.md)

- **PROJECT_ID**: `gravity_core`
- **VERSION**: `v1`
- **方針承認**: Agent-1 (CEO / 統括部長), Agent-2 (開発部長)
- **策定担当**: Agent-2-assist (開発部長補佐)
- **監査承認**: Agent-1-assist (統括部長補佐 / Chief Architect)
- **物理書き込み**: Agent-3-C (ファイル管理者)

---

## 1. 開発目的および全体方針

本プロジェクトの目的は、GRAVITY Multi-Agent Organization Specification v6.0（Thought Support OS / Hierarchical Execution Engine）に完全準拠したコアシステム基盤の構築、各課の責務定義、および高品質な実行ドキュメント・成果物（`completion.md`）の策定である。

### 【基本方針】
1. **完全隔離 (Project Isolation)**: 他プロジェクトとのコンテキスト混入を完全に排除し、`projects/gravity_core/v1/` 配下で完結させる。
2. **完全直列実行 (Serialized Pipeline)**: 全処理をシングルステップ直列で進行し、中間ステート・要約を `company_state.json` に同期する。
3. **成果物の一元管理**: 最新成果物は固定名 `completion.md` とし、履歴は `history/` に退避する。

---

## 2. 課別マクロ指示

### 【プロンプト課 (SECTION_2_PROMPT) への指示】
- **Agent-2-P** による課内統括のもと、以下の成果物を策定すること：
  - **アーキテクチャ・構造定義 (担当: Agent-2-P1)**:
    - システムの3-SA（SA1, SA2, SA3）連携フローの定義
    - ガード制御およびプロンプト境界条件（PUBLIC/PRIVATE分離ルール）の厳格定義
  - **ペルソナ・トーン設計 (担当: Agent-2-P2)**:
    - 各エージェント（Agent-1〜Agent-3系）の厳密な呼称・役職・言語トーンの策定
    - 外部向け（PUBLIC）の簡潔・格調高い報告トーンの策定

### 【コード課 (SECTION_2_CODE) への指示】
- **Agent-2-C** による課内統括のもと、以下の成果物を策定すること：
  - **ロジック・エンジン処理仕様 (担当: Agent-2-C1)**:
    - 状態遷移管理（State Database I/O）アルゴリズム
    - 可変修正ループ（Adaptive Repair Loop / 収束度評価・LEVEL 1〜3 遷移ロジック）の仕様設計
  - **フォーマット整形・名義変換仕様 (担当: Agent-2-C2)**:
    - ログファイル、QA判定カード、差分ログ（Append-Only）のフォーマットテンプレート策定
    - ハイフン繋ぎのエージェント名統一チェック仕様

---

## 3. 品質保証部 (QA) 連携要件

- QA部（Agent-3-A）は本マクロ指示書および次フェーズのミクロ指示書からすべての要件を「1要件＝1テストケース」に完全分解すること。
- 検品係（Agent-3-B）による全項目直列判定で PASS を取得すること。
