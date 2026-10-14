# GRAVITY MULTI-AGENT ORGANIZATION SPECIFICATION v6.0 システム完成成果物 (completion.md)

- **PROJECT_ID**: `gravity_core`
- **ACTIVE_VERSION**: `v1`
- **システムモード**: Thought Support OS / Hierarchical Execution Engine
- **作成担当**: 開発部全作業員 (Agent-2-P1, Agent-2-P2, Agent-2-C1, Agent-2-C2)
- **統括・物理保存**: Agent-3-C (ファイル管理者 / Storage Guardian)
- **最終承認**: Agent-1 (CEO / 統括部長)

---

## 1. エグゼクティブ・サマリー

本システム成果物は、「GRAVITY Multi-Agent Organization Specification (Version 6.0 - 3-SA Triple Assist & Storage Guardian Architecture)」に基づき、完全直列実行パイプライン、厳格なPUBLIC/PRIVATE分離、状態管理データベース同期、および可変修正ループを備えた階層型エージェント実行基盤を定義・実装したものである。

---

## 2. システム・アーキテクチャ概要

### 2.1 ディレクトリ・ストレージ構造
すべてのデータおよび中間ログは、プロジェクトルート `projects/gravity_core/v1/` 配下に完全隔離保持される。

```text
projects/gravity_core/v1/
├── company_state.json                 # 最新状態データベース (State DB)
└── files/
    ├── achievements/                  # 完成成果物ストレージ
    │   ├── completion.md              # 常に最新の完全な完成成果物（固定名）
    │   └── history/                   # 過去成果物退避ストレージ
    └── reports/                       # プロセス・指示・ログストレージ
        ├── 00_static_audit.md         # 静的監査レポート
        ├── 01_plan.md                 # 全体計画書
        ├── 02_outline_work.md         # 大枠指示書
        ├── 06_fix_reason.md           # 修正理由・差分ログ (Append-Only)
        └── history/                   # イテレーション履歴ストレージ
            └── step_01/
                ├── 03_detail_work.md  # 詳細指示書
                ├── 04_working_log.md  # 作業員作業ログ
                └── 05_qa_test.md      # QAテストスイート・検品結果
```

---

## 3. 組織レイヤー定義と責務マトリクス

### 3.1 統括部 (Team 1 Leadership: 3-SA Triple Assist)
| エージェント | 役割 | 専任機能 / ガード条件 |
| :--- | :--- | :--- |
| **Agent-1** | CEO / 統括部長 | 意思決定・最終承認専任。ドキュメント直接執筆厳禁。PUBLIC報告主幹。 |
| **Agent-1-assist** | 統括部長補佐 (Chief Architect) | マクロ設計査定、静的設計監査承認、LEVEL 2 リカバリ主導。執筆厳禁。 |
| **Agent-1-sub-assist-1** | 統括部システム副補佐 (SA1) | `company_state.json` 更新および Agent-3-C への物理 I/O 指示専任。 |
| **Agent-1-sub-assist-2** | 統括部進行副補佐 (SA2) | タスク分解、動的アサイン、動作テスト（動的実行検証）。 |
| **Agent-1-sub-assist-3** | 統括部品質・Doc副補佐 (SA3) | 1次静的監査 (1st-Audit)、`00_*.md` Draft作成、課題集約。 |

### 3.2 開発部 (Team 2 Dynamic Layer)
- **Agent-2** : 開発部長（判断・承認専任）
- **Agent-2-assist** : 開発部長補佐（マクロ指示書作成、現場成果物要約）
- **プロンプト課 (SECTION_2_PROMPT)**:
  - **Agent-2-P** : プロンプト課長（判断・承認専任）
  - **Agent-2-P-assist** : プロンプト課長補佐（ミクロ指示書作成、要約・比較）
  - **Agent-2-P1** : プロンプト・アーキテクト（構造定義、指示条件、ガード制御）
  - **Agent-2-P2** : ペルソナ・トーンデザイナー（ペルソナ設定、呼称設定、トーン制御）
- **コード課 (SECTION_2_CODE)**:
  - **Agent-2-C** : コード課長（判断・承認専任）
  - **Agent-2-C-assist** : コード課長補佐（ミクロ指示書作成、要約・比較）
  - **Agent-2-C1** : ロジック・エンジンエンジニア（コア計算、エンジン処理、状態遷移）
  - **Agent-2-C2** : テキスト・フォーマットエンジニア（整形、名義変換、用語置換）

### 3.3 品質保証部 (Team 3 QA Layer)
- **Agent-3** : QA部長（判断・承認専任）
- **Agent-3-assist** : QA部長補佐（テスト・不具合要約、判定カード生成）
- **Agent-3-A** : テスト作成者（1要件＝1テストケース最小粒度完全分解）
- **Agent-3-B** : 検品係（現場提出物に対する1項目直列判定・不具合分類付与）
- **Agent-3-C** : ファイル管理者（Storage Guardian / ファイルツリー物理同期・退避制御）

---

## 4. 実行プロトコル & ガードレール

### 4.1 完全直列パイプライン (Serialized Pipeline)
各ステップは以下の直列順序でのみ実行され、各フェーズのテスト合格をもって次フェーズへ進む：
1. `BOOTSTRAP & ANALYSIS` ➔ テストパス ➔ `company_state.json` 同期
2. `MACRO_INSTRUCTION` (`02_outline_work.md`) ➔ テストパス ➔ State 同期
3. `MICRO_INSTRUCTION` (`03_detail_work.md`) ➔ テストパス ➔ State 同期
4. `WORKER_EXECUTION` (`04_working_log.md` & `completion.md`) ➔ テスト設計・検品 (`05_qa_test.md`) ➔ State 同期
5. `TRIPLE CHECK PROTOCOL` (動的検証 ➔ 静的監査 ➔ 最終承認) ➔ 完了

### 4.2 可変修正ループ (Adaptive Repair Loop)
- **LEVEL 1 (局所修正)**: 分類が「局所・プロンプト/コード」の場合、Diff指示書により修正。
- **LEVEL 2 (構造再設計)**: 分類が「広汎/構造」またはLEVEL 1停滞時、Agent-1-assist がマクロ再設計。
- **LEVEL 3 (人間引き継ぎ)**: 発散停止不能時、不完全な成果物は出力せず人間へエスカレーション。

### 4.3 表側出力インターフェース規約
- **[PUBLIC] チャット出力**:
  全タスク正常完了時、以下のみを出力する：
  ```text
  【統括部長報告】 
  QA 検品およびすべてのタスクが正常に完了しました。
  ```
- 思考プロセス、ログ、指示書はすべて PRIVATE（ファイルシステム）上でのみ管理する。
