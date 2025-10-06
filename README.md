概要

単一ファイル（index.html）で動くシンプルTodo

追加／削除／完了チェック、表示フィルター、LocalStorage自動保存

モダンUI・ダークモード・丁寧コメント入り

学べること

DOM操作／イベントリスナー（submit, click, change, 委譲）

LocalStorage（setItem/getItem + JSON.stringify/parse）

配列操作（push/find/filter/map）

軽量SPAの描画フロー（render()）

要件

ブラウザ：最新の Chrome / Edge / Firefox / Safari

エディタ：VS Code（推奨：Live Server）

クイックスタート（VS Code）

フォルダ作成 → index.html を作る

コードを全貼り → 保存

開く（ダブルクリック or Live Server）

使い方

入力 → 追加

✅で完了切替／🗑️で削除

フィルター：すべて／未完了／完了

自動保存：LocalStorage

仕様（期待動作）

空白のみは追加しない

タイトル最大 120 文字

削除はワンクリック（確認なし）

表示時は escapeHTML で & < > " ' をエスケープ

保存キー：simple-todo-v1

タスク構造：{id, title, completed, createdAt}

テスト

コンソールでユニットテスト常時実行（escapeHTML）

#test をURL末尾に付けると統合テスト実行（追加/切替/削除/フィルター）

実行後は状態を復元

通常：Stateful tests: SKIPPED

#test：Stateful tests: PASSED

ディレクトリ

ルートに index.html 1枚のみ

コード構成

状態：tasks / currentFilter / storageKey

永続化：load() / save()

描画：render()

操作：addTask() / toggleTask() / deleteTask()

ユーティリティ：escapeHTML()

イベント：submit / click（委譲） / change / フィルターボタン

アクセシビリティ

aria-* / role / sr-only

フォーカスリング・ダークモード対応

セキュリティ

文字列は escapeHTML 経由で無害化

インライン <script> での </script> は分割して扱う

トラブルシューティング

保存されない：シークレットモード・ストレージ設定確認

真っ白／動かない：Consoleのエラー確認

文字列エラー：貼り付け重複や </script> の扱いを確認

カスタマイズ例

カラー／角丸／影（CSS変数）・最大文字数・保存キー

削除確認ダイアログ・編集機能・タグ/期日・検索・並び替え

発展課題

インライン編集、完了一括削除、ドラッグ&ドロップ、JSON入出力
