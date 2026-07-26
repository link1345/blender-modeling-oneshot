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

次の3Dモデルを作成してください。

## 参照資料

- 見本のイメージ画像: 添付画像の通り
- 現在モデルの正面画像: 添付画像の一番左の絵
- 現在モデルの側面画像: 添付画像の左から２つ目の絵
- 時計部分の細部: 添付画像の一番右の列にある一番上の絵
- 時計と鍵をつなぐ部分の細部: 添付画像の一番右の列にある上から２番目の絵
- 鍵の部分の細部: 添付画像の一番右の列にある上から３番目の絵

## 制作対象
「銀装飾の黒い物理演算で揺れるアンティーク鍵」の3Dモデルを作ってほしいです。
- 小道具の役割 : 装飾品 
- 装着場所と持ち方 : 髪につけるが、やや浮遊する形でつける 
デザインの方向性 : 機械仕掛け風
- 色と素材 : 黒・白・銀を基本に、髪と瞳に合わせた青を差し色にしてほしい。ガラス系の表現にしてほしい 
- 実装条件 : VRM限定で使う。着脱できるようにする予定なので、アイテムの3DモデルはFBX形式で単独で作ってほしい。(モデルとは別に作る)。シェーダーはBlenderに登録してあるVRMのシェーダーを使ってください。 
- その他 : デザインできればで良いのですが、下記リンク先のVRMのテクスチャを動かす技術を用いて、時計の針(秒針は60等分・時針は12等分)で「チクチク」と時間表現をしてほしいです。時計の針は、板ポリゴンで表現できるレベルだと思うので、板ポリゴンで表現してください。 
[https://note.com/what_wat_/n/n01daa21e0400](https://note.com/what_wat_/n/n01daa21e0400)

### モデル用途
VRMモデルにつける3Dモデルのアクセサリー。
しかし、今回はFBX形式前提での作成で良い。

## 参照資料

- 正面: 添付画像の一番左の絵 
- 側面: 添付画像の左から２つ目の絵 
- 背面: 添付画像の左から３つ目の絵
- 時計部分の細部: 添付画像の一番右の列にある一番上の絵
- 時計と鍵をつなぐ部分の細部: 添付画像の一番右の列にある上から２番目の絵
- 鍵の部分の細部: 添付画像の一番右の列にある上から３番目の絵

参照画像に存在しない部分を推測する場合は、
推測した内容を実装前の計画で明示してください。

## 作業規則

- Blenderを変更できるのはBlender Modelerだけです。
- Visual Analyst、Planner、Visual Reviewer、Geometry Inspectorは変更してはいけません。
- 修正前に必ず別名のチェックポイントを保存してください。
- Modeler完了後にVisual ReviewerとGeometry Inspectorを独立して実行してください。
- 修正前後を比較し、IMPROVED / NEUTRAL / REGRESSEDを判定してください。
- NEUTRALまたはREGRESSEDなら候補を採用しないでください。
- 同じ問題で3回失敗した場合は作業を止め、原因を報告してください。
- 指定されていない装飾を追加しないでください。

まずは読み取り専用のVisual Analystによる比較分析から開始してください。
Plannerが限定的な修正計画を作り、
Coordinatorが承認するまでBlenderを変更しないでください。