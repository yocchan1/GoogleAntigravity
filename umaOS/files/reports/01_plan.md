# プロジェクト全体計画書 (01_plan.md)

- **PROJECT_ID**: `gravity_core`
- **VERSION**: `v1`
- **モード**: Thought Support OS / Hierarchical Execution Engine
- **作成担当**: Agent-1-sub-assist-2 (進行副補佐)
- **物理書き込み**: Agent-3-C (ファイル管理者 / Storage Guardian)
- **承認**: Agent-1 (CEO / 統括部長), Agent-1-assist (統括部長補佐)

---

## 1. 組織体制・役割アサイン

### 【統括部 (Team 1 Leadership)】
- **Agent-1** : CEO / 統括部長（意思決定・最終承認専任、判断のみ）
- **Agent-1-assist** : 統括部長補佐 (正補佐 / Chief Architect)（マクロ設計査定・承認、LEVEL 2 リカバリ）
- **Agent-1-sub-assist-1 (SA1)** : 統括部システム副補佐（State DB 管理、Background Task 制御、I/O 指示発行）
- **Agent-1-sub-assist-2 (SA2)** : 統括部進行副補佐（タスク分解、動的アサイン、動的実行検証）
- **Agent-1-sub-assist-3 (SA3)** : 統括部品質・ドキュメント副補佐（1次静的監査、00_*.md 初稿作成、課題整理）

### 【開発部 (Dynamic Layer Structure)】
- **Agent-2** : 開発部長（判断・承認専任）
- **Agent-2-assist** : 開発部長補佐（統括部タスク受領、課別マクロ指示書策定、成果物要約）
- **[SECTION_2_PROMPT] (プロンプト課)**:
  - **Agent-2-P** : プロンプト課長（判断・承認専任）
  - **Agent-2-P-assist** : プロンプト課長補佐（ミクロ指示書策定、要約・比較）
  - **Agent-2-P1** : プロンプト・アーキテクト（構造定義、指示条件、ガード制御）
  - **Agent-2-P2** : ペルソナ・トーンデザイナー（ペルソナ設定、愛称・呼称設定）
- **[SECTION_2_CODE] (コード課)**:
  - **Agent-2-C** : コード課長（判断・承認専任）
  - **Agent-2-C-assist** : コード課長補佐（ミクロ指示書策定、要約・比較）
  - **Agent-2-C1** : ロジック・エンジンエンジニア（コア計算、エンジン処理）
  - **Agent-2-C2** : テキスト・フォーマットエンジニア（名義変換、口調適用、用語置換、フォーマット整形）

### 【品質保証部 (Team 3 QA)】
- **Agent-3** : QA部長（判断・承認専任）
- **Agent-3-assist** : QA部長補佐（テスト・不具合要約、判定カード生成）
- **Agent-3-A** : テスト作成者 (Test Architect)（1要件1ケース完全分解・テストスイート起票）
- **Agent-3-B** : 検品係 (Test Inspector)（1項目直列判定、合否・不具合分類付与）
- **Agent-3-C** : ファイル管理者 (Storage Guardian)（ファイルツリー物理検証、バージョン退避、Append-Only 制御）

---

## 2. 全体実行フロー (完全直列パイプライン)

1. **Phase 1: BOOTSTRAP & ANALYSIS**
   - ディレクトリ構造および初期ステート DB (`company_state.json`) の生成
   - 全体計画書 (`01_plan.md`) の策定
   - Agent-1-SA1 / Agent-3-C による初期化ステート保存
2. **Phase 2: MACRO_INSTRUCTION (大枠指示策定)**
   - Agent-1 方針承認のもと、Agent-2-assist がマクロ指示書 (`02_outline_work.md`) を策定
   - Agent-1-assist によるマクロ設計監査・承認
   - ステート更新保存
3. **Phase 3: MICRO_INSTRUCTION (詳細指示策定)**
   - 各課課長（Agent-2-P, Agent-2-C）承認のもと、各課長補佐がミクロ指示書 (`history/step_01/03_detail_work.md`) を策定
   - テストパスおよびステート更新保存
4. **Phase 4: WORKER_EXECUTION & QA INSPECTION (作業実行＆検品)**
   - 各作業員（P1, P2, C1, C2）による作業実行ログ (`04_working_log.md`) および完成成果物 (`completion.md`) の作成
   - Agent-3-A による1要件1ケース最小粒度テスト設計起票 (`05_qa_test.md`)
   - Agent-3-B による1項目直列照合検品・判定カード確定
5. **Phase 5: TRIPLE CHECK PROTOCOL (統括部トリプルチェック)**
   - Check 1: Agent-1-SA2 による動的実行検証
   - Check 2: Agent-1-SA3 による1次静的監査 (`00_static_audit.md`) ➔ Agent-1-assist による最高位静的承認
   - Check 3: Agent-1 (CEO) による最終承認宣言 ➔ Agent-1-SA1 / Agent-3-C によるステート更新・物理同期
6. **Phase 6: FINAL DELIVERABLE & PUBLIC REPORT**
   - チャット（PUBLIC）への規定フォーマットによる完了報告
