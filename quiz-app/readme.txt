## README.md
```md
# PHP Quiz App (MAMP)

シンプルな日本語 UI のクイズアプリ。MAMP + PHP + MySQL で動作します。

## 1) 必要環境
- Windows 11 + MAMP
- PHP 8.x / MySQL 8 目安

## 2) セットアップ
1. MAMP を起動し、MySQL のポートを確認（デフォルト 8889）。
2. phpMyAdmin でデータベース `quiz_db` を作成。
3. `sql/schema.sql` を上から順に実行。
   - `admins` への INSERT はハッシュが必要です。`admin/make_hash.php` を一時的に起動し、得られたハッシュをコピペしてください（下記参照）。
4. `includes/db.php` の接続設定（ユーザー/パス/ポート）を環境に合わせて調整。
5. MAMP の Document Root を `quiz-app/public` に設定、またはエイリアス設定。
6. ブラウザで `http://localhost:8888/`（ポートは環境により異なる）へ。

## 3) 管理者パスワードの作成
`admin/make_hash.php` にアクセス → パスワードを入力 → 生成されたハッシュを `sql/schema.sql` の `REPLACE_WITH_HASH` に貼り付けて INSERT を実行。
※ セキュリティ上、ハッシュ作成後は `make_hash.php` を削除してください。

## 4) 初期データ
- カテゴリ：HTML / CSS（例）
- 各カテゴリに 4 問のサンプル（必要に応じて追加）

## 5) 動作の流れ
- `/` でカテゴリを選択 → `/quiz.php?category_id=...` で 10 問まで（不足時は全件）ランダム出題
- 各問の回答後に正誤表示（不正解時は正解＆解説） → 次の問題
- 終了時にスコア表示
- `/admin/login` でログイン → 質問/カテゴリの CRUD

## 6) 備考
- CSRF 対策、プリペアドステートメント、XSS エスケープを実装
- スタイルは寒色系・モバイル優先
- 実運用前に `admin/make_hash.php` は必ず削除
