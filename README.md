シンプルTodo（単一HTML・ローカル保存・SPA）

単一の index.html だけで動くシンプルなTodoアプリです。
タスクの 追加 / 削除 / 完了チェック、表示の フィルター（すべて／未完了／完了）、LocalStorage による自動保存を備えています。
UI はモダンでダークモードにも対応。コードには 中学生でも理解できる丁寧なコメントが入っています。

目次

デモとゴール

主な機能

学べること

動作要件

クイックスタート（VS Code）

使い方

仕様（期待される動作）

テストの実行

ディレクトリ構成

コード構成

アクセシビリティ

セキュリティ

トラブルシューティング

カスタマイズ

発展課題の例

ライセンス

デモとゴール

ブラウザで index.html を開くだけで動作します。

目標：DOM操作・イベント・LocalStorage・配列操作の基本を、動くUIで楽しく学ぶこと。

主な機能

タスクの 追加・削除・完了チェック

フィルター（すべて / 未完了 / 完了）

LocalStorage による自動保存（ページを閉じても残る）

モダンUI（ガラス風カード、やわらかい影、ダークモード対応）

イベントデリゲーションで軽量なリスナー構成

XSS耐性（タイトル表示に escapeHTML を使用）

学べること

基本的なDOM操作：要素取得、innerHTML での描画

イベントリスナー：submit / click / change、委譲（バブリング）

LocalStorage API：setItem / getItem と JSON.stringify / parse

配列操作：push / find / filter / map

軽量SPAの描画フロー（render() の考え方）

動作要件

ブラウザ：最新の Chrome / Edge / Firefox / Safari

エディタ：VS Code（推奨拡張：Live Server）

クイックスタート（VS Code）

任意のフォルダを作成（例：to-do list/）。

フォルダ内に index.html を 1 ファイル作成。

本リポジトリ（またはキャンバス）のコードを まるごと貼り付けて保存。

実行方法

そのままファイルをダブルクリックして開く

もしくは VS Code の Live Server で「Open with Live Server」

使い方

入力欄にタスクを入力して 「追加」。

✅ をクリックで 完了／未完了 を切り替え。

🗑️ をクリックで 削除。

右上の フィルター で表示切替（すべて／未完了／完了）。

データは自動で LocalStorage に保存。

仕様（期待される動作）

空白のみの入力は無視（" " などは追加されない）

タイトルは 最大120文字

削除は ワンクリックで即時（確認ダイアログなし）

文字表示は escapeHTML により & < > " ' をエスケープ
→ 属性・HTML文脈での不正混入を防止

タスク構造

type Task = {
  id: string;        // ランダムID（時刻+乱数）
  title: string;     // タスク名
  completed: boolean;// 完了フラグ
  createdAt: number; // 生成時刻（ms）
}


LocalStorage キー：simple-todo-v1

テストの実行

本プロジェクトは 簡易テスト を内蔵しています（コンソール出力）。

1) ユニットテスト（常時実行）

escapeHTML の変換結果を検証。

2) 統合テスト（任意・URLフラグ）

URL の末尾に #test を付けて開くと実行。例：

file:///.../index.html#test


追加/切替/削除/フィルター表示の件数整合などを検証。

実行後は 元のタスクと LocalStorage を復元。

期待されるコンソール出力

通常時：Stateful tests: SKIPPED (add #test to URL to run)

#test 付き：Stateful tests: PASSED → All tests: PASSED

ディレクトリ構成
/
└─ index.html    # HTML/CSS/JS/テストが1ファイルに同梱

コード構成

状態と設定

storageKey：LocalStorage のキー

tasks: Task[]：タスク配列

currentFilter: 'all' | 'active' | 'completed'

永続化

load() / save()

描画

render()：フィルターに応じて tasks → HTMLへ

操作

addTask(title) / toggleTask(id) / deleteTask(id)

ユーティリティ

escapeHTML(str)：[&<>"'] をすべてエスケープ

イベント

submit：追加

click（委譲）：削除ボタン

change（委譲）：チェックボックス

フィルター切替ボタン群

アクセシビリティ

aria-label / aria-live / role="application" の付与

視覚的には非表示だがスクリーンリーダーに読む sr-only ラベル

フォーカス時のリング表示・コントラスト配慮

ダークモード対応（prefers-color-scheme）

セキュリティ

タイトル描画時に escapeHTML を必ず通すことで、
<script> などの文字列を無害化（&lt;script&gt; へ変換）

インライン <script> の中で </script> を扱うテストは 文字列分割（'</' + 'script>'）で安全に記述

トラブルシューティング

保存されない：シークレットモードやストレージ制限に注意。
→ ブラウザ通常モードで再確認、またはストレージ設定を見直し。

動かない／真っ白：開発者ツールの Console を開いてエラーを確認。

文字列が途中で終わるエラー（Unterminated string literal など）：
→ コードの貼り付け時に 重複や抜けがないか、特にテスト部分を確認。

</script> を含む文字列を直接書かない：テストでは分割済み。独自に追加する場合も同様に。

カスタマイズ

スタイル：CSS の :root 変数（色・角丸・影）を調整

最大文字数：maxlength を変更

保存キー：storageKey を変更

削除の確認：deleteTask 呼び出し前に confirm(...) を挟む

項目の拡張：期日・タグ・優先度・並び替え などをフィールド追加

発展課題の例

編集機能：タイトルをクリック→インライン編集

並び替え：ドラッグ＆ドロップでの並べ替え

完了一括削除：completed === true をまとめて削除

検索：タイトル部分一致でフィルタリング

エクスポート/インポート：JSON でバックアップ
