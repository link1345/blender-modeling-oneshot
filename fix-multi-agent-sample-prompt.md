Use the `blender-modeling` skill and its multi-agent correction workflow for this task.

あなたはCoordinatorとして作業してください。

最初に以下を読んでください。

- `.agents/skills/blender-modeling/references/multi-agent-workflow.md`
- `.agents/skills/blender-modeling/workflow.yaml`
- `.agents/skills/blender-modeling/templates/iteration-state.yaml`

各担当が必要になった段階で、
`.agents/skills/blender-modeling/agent-prompts/`
にある対応する役割設定を読んでください。

## 目的

参照画像と現在の3Dモデルを比較し、形状の違和感を局所的に修正してください。

## 人間からの指摘

時計下部の接続部が、見本より団子のように膨らみすぎています。
棒は以前より良くなったので、なるべく維持してください。

人間へ正確な寸法を質問せず、
参照画像から相対的な修正量を推定してください。

## 参照資料

- 見本画像: `[見本画像のパス、または添付画像]`
- 現在モデルの正面画像: `[正面画像のパス、または添付画像]`
- 現在モデルの側面画像: `[側面画像のパス、または添付画像]`
- 現在モデルの斜め画像: `[斜め画像のパス、または添付画像]`
- 現在のBlenderファイル: `[現在採用中のblendファイル]`

## 修正対象

時計本体下部の接続金具。

## 維持する部分

- 時計盤
- 時計外枠
- 上部リング
- 主軸の長さ
- 鍵歯
- 全体の縦長シルエット

## 評価対象外

- 色
- 材質
- テクスチャ
- ライティング

## 作業規則

- 一度に修正する主要問題は1件だけにしてください。
- Blenderを変更できるのはBlender Modelerだけです。
- Visual Analyst、Planner、Visual Reviewer、Geometry Inspectorは変更してはいけません。
- 修正前に必ず別名のチェックポイントを保存してください。
- Modeler完了後にVisual ReviewerとGeometry Inspectorを独立して実行してください。
- 修正前後を比較し、IMPROVED / NEUTRAL / REGRESSEDを判定してください。
- NEUTRALまたはREGRESSEDなら候補を採用しないでください。
- 同じ問題で3回失敗した場合は作業を止め、原因を報告してください。
- 指定されていない装飾を追加しないでください。
- 修正対象外の部分を作り直さないでください。

まずは読み取り専用のVisual Analystによる比較分析から開始してください。
Plannerが限定的な修正計画を作り、
Coordinatorが承認するまでBlenderを変更しないでください。