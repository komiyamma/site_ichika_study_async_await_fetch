# 📁 previous_lesson (学習済み内容) の状況整理

このファイルは、新規学習プロジェクト（ルートディレクトリ）と、生徒が学習済みの内容（`previous_lesson` ディレクトリ）を明確に区別し、混同を避けるための覚書です。

## 👩‍🎓 生徒のプロフィール
- **属性**: 文系女子学生。
- **学習歴**: 4ヶ月。
- **経験**: IT、プログラミング（HTML/CSS/JS）ともに今回が初学者。
- **現在地**: 以下の「毎日の運動トラッカー」アプリを自力で完成させた直後。

## 🏁 完了したプロジェクト:「毎日の運動トラッカー」
- **格納場所**: `./previous_lesson/` フォルダ内
- **使用技術**:
  - HTML5 / CSS3 (Bootstrap版もあり)
  - Vanilla JavaScript
  - `localStorage` (データの永続化に使用)
- **達成したこと**:
  - フォームからの入力受け取り
  - 配列とオブジェクトを使ったデータ管理 (`script.js`参照)
  - DOM操作によるテーブル描画
  - データの一覧表示、フィルタリング、削除機能

## ✨️ 理解した「previous_lesson」教材の中身（要約）
### 教材ファイル（解説）
- `./previous_lesson/D00.md`：14日ロードマップ（localStorage→表示→削除→フィルタ→Bootstrap→仕上げ→手動テスト）
- `./previous_lesson/D01.md` から `./previous_lesson/D15.md`：ストーリー形式で段階的に実装を進める解説（Day12がBootstrap、Day13が仕上げ、Day14が手動テスト）
- `./previous_lesson/README.md`：教材入口・2つのUI版の説明（どちらも同じ `script.js` を使う）

### アプリ画面（HTML）
- `./previous_lesson/index.html`：シンプル版（素のHTML + 最小限CSS）
- `./previous_lesson/index.bootstrap.html`：Bootstrap版（見た目だけBootstrap、ロジックは同じ `script.js`）

### アプリ本体（JavaScript）
- `./previous_lesson/script.js`：localStorage完結のCRUD + フィルタ + 描画の完成版
  - 保存キー：`ichikaWorkoutLogEntries`（`WORKOUT_STORAGE_KEY`）
  - データ形：`WorkoutEntry`（`id`, `date`, `type`, `minutes`, `value`, `note`, `createdAt`）
  - 起動：`DOMContentLoaded` → `initializePage()`（要素取得→イベント登録→日付初期化→一覧描画）
  - 追加：フォーム `submit` を `preventDefault()` し、入力から `entry` を作って配列へ追加→`JSON.stringify`で保存→フォームreset→再描画
  - 表示：`renderEntryTable()`（日付フィルタ `filter-date` があれば一致で絞り込み、`createdAt` 降順で並べて `tbody#list` に `innerHTML` 反映）
  - 削除：行ボタン `onclick` → `removeEntryById()` → 再描画
  - デバッグ全削除：確認ダイアログ後、該当キーのみ `localStorage.removeItem`
  - XSS対策：`escapeHtml()` を通してから `innerHTML` に投入
- `./previous_lesson/theme-toggle.js`：`data-bs-theme` と `localStorage` による light/dark 切替の部品（`index.bootstrap.html` 側には現状読み込みが無いので、組み込み前提の補助ファイルという位置づけ）

## ⚠️ 【重要】ファイル構成の注意点
**ルートディレクトリと `previous_lesson` ディレクトリには、同名のファイル（`D00.md` ～ `D15.md`）が存在しますが、中身は全く別の教材です。**

| 場所 | フォルダ | 内容 | テーマ |
| :--- | :--- | :--- | :--- |
| **今回の教材** | `(root)/` | **新・Webアプリ開発講座** | **非同期処理 (Promise, async/await), Fetch API** |
| **過去の教材** | `previous_lesson/` | 毎日の運動トラッカー | DOM操作, localStorage, 配列操作 |

### 取り扱いルール
1. **過去の参照**: 生徒の前提知識（「ここまでなら分かる」）を確認する際は、必ず `previous_lesson/` 内のファイルを参照すること。
2. **新規作成**: 今後の学習（非同期処理など）に関する解説やコードは、**ルートディレクトリ** の `Dxx.md` や `script.js` (もし作成するなら) で行うこと。
3. **混同防止**: 例えば「D05を見る」という指示があった場合、それが「過去の振り返り(previous_lesson)」なのか「新しい非同期の話(root)」なのかを文脈から厳密に判断すること。

---
*このファイルは AI アシスタントがコンテキストを正しく維持し、生徒の学習段階を見誤らないために作成されました。*
