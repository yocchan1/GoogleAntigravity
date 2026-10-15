# 修正理由・差分ログ (06_fix_reason.md)

- **PROJECT_ID**: `gravity_core`
- **ルール**: 末尾追記（Append-Only）のみ許可。上書き・差分置換厳禁。
- **物理管理**: Agent-3-C (ファイル管理者 / Storage Guardian)

---

## [v0 → v1]

### 1. 修正・初期構築要約
- **不具合分類**: `広汎・構造`（初期ベースライン構築）
- **原因**: 初期リポジトリ未初期化状態からのブートストラップ要件
- **修正内容**: GRAVITY Multi-Agent Architecture v6.0 の全体系（Leadership 3-SA, Dynamic Layer, QA Layer, State DB, 成果物）の初期構築・完全直列パイプライン展開

### 【修正前】
```text
(空のワークスペース - 未初期化状態)
```

### 【修正後】
```text
projects/gravity_core/v1/
├── company_state.json
└── files/
    ├── achievements/
    │   ├── completion.md
    │   └── history/
    └── reports/
        ├── 01_plan.md
        ├── 02_outline_work.md
        ├── 06_fix_reason.md
        └── history/
            └── step_01/
                ├── 03_detail_work.md
                ├── 04_working_log.md
                └── 05_qa_test.md
```


---

## [v1 → v2]

### 1. 修正要約
- **不具合分類**: `広汎・プロンプト`
- **原因**: 添付された「統合対話制御システム仕様プロトコル」における枝番混在（21-a, 36-a〜i 等）、Phase 0 と Phase 1.2 の循環参照、およびプロンプト境界条件の曖昧性
- **修正内容**:
  1. 全規則を「1要件＝1判断」のアトミック規則通し番号（規則 001 〜 147）に完全フラット化。
  2. ターン0ペルソナ完全凍結とパース・外部調査・カテゴリ/愛称確定の時系列直列化による循環参照の完全排除。
  3. LLM生成（Phase 7）とPython決定論的処理（Phase 1〜6.5）の責務分離およびシステムガードの厳密化。

### 【修正前】
```markdown
## Phase 1.2: パース・動的抽出・補完（アトミック規則）
...
21. fullname_en は、公式サイトに必ず存在する英語表記を、fullname の英字の有無にかかわらず常に検索により取得する。  
21-a. fullname_en は姓名の区切りを示すスペースを保持した状態で保存し、slug化（区切りの除去）は姓名境界の確定後に行う。  

### nicknameの導出
...
36. category が 「other」 でカタカナを含まない場合、fullname_kana および nickname をPython関数 derive_kana_from_fullname_en により導出する。  
36-a. 姓名の境界は、Python関数 resolve_name_boundary により、fullname_en（スペース区切りを保持）から決定論的に確定する。  
36-b. fullname にひらがなの塊があり、その読みが fullname_en のいずれかのトークンと一致する場合...
```

### 【修正後】
```markdown
## Phase 1.2: パース・動的抽出・補完（アトミック規則）
...
030. fullname_en は、公式サイトに存在する英語表記を検索により取得する。  
031. fullname_en は姓名の区切りを示すスペースを保持した状態で保存する。  
032. agent_slug は、Python関数 build_slug_from_fullname_en により fullname_en から姓名境界確定後に生成する。  
033. agent_slug の構成文字は、a-zの英字小文字のみとし、数字を含めない。  

### nicknameの導出（直列優先度評価）
...
050. category が other でカタカナを含まない場合、Python関数 resolve_name_boundary により fullname_en（スペース保持）から姓名境界を確定する。  
051. fullname 内のひらがなの塊と fullname_en のいずれかのトークンのヘボン式ローマ字読みが一致する場合、その位置関係に基づき姓・名を確定する。  
052. ひらがな一致による判定が不可能な場合、name_order="family_first" に基づきトークンの並びから姓・名を確定する。  
```
