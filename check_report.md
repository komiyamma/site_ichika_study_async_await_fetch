# コード動作確認レポート

各ファイルを確認した結果、以下の箇所で「そのままコピペしても動かない（未定義の関数や変数がある）」ため、補足やダミー関数の定義が必要と思われる箇所が見つかりました。

特に **Day 6 ～ Day 9** は「概念的な関数のチェーン」が中心のため、実際に動かして試したい学習者のために、各ファイルの冒頭または該当箇所に「実験用ダミー関数セット」を記載することをお勧めします。

## 📋 修正推奨箇所リスト

### 1. D06.md (Promise / .then)
- **現状**: `orderCoffee()`, `drink(coffee)`, `download()`, `process()`, `display()` が未定義のまま使われています。
- **提案**: 「以下のダミー関数をコンソールに貼り付けてから実験してね」という補足を追加するか、コードブロック内に定義を含める。

```javascript
// 【実験用ダミー関数】
function orderCoffee() { return Promise.resolve('☕ コーヒー'); }
function drink(coffee) { console.log(coffee + 'を飲みました'); }
function download() { return Promise.resolve('データ'); }
function process(data) { return Promise.resolve(data + 'を加工'); }
function display(data) { console.log(data + 'を表示'); }
```

### 2. D07.md (async/await)
- **現状**: `download()`, `process()`, `display()`, `orderCoffee()` に加え、`dangerousWork()` (Line 128) が未定義です。
- **提案**: D06同様のダミー定義が必要です。特に `dangerousWork()` は「失敗する」パターンも見せたい場合、以下のような定義が必要です。

```javascript
// async/await 実験用
const download = () => new Promise(r => setTimeout(() => r('データ'), 1000));
const process = (d) => new Promise(r => setTimeout(() => r(d + '加工'), 1000));
const display = (d) => console.log(d + '表示');
// 失敗する関数
const dangerousWork = () => Promise.reject('爆発しました💥');
```

### 3. D08.md (try...catch)
- **現状**: `showLoadingSpinner()`, `downloadData()`, `showData()`, `showError()`, `hideLoadingSpinner()` (Line 115周辺) が未定義です。
- **提案**: これらは `finally` の挙動（成功/失敗にかかわらず実行）を確認するために重要です。

```javascript
// try-catch 実験用
const showLoadingSpinner = () => console.log('🌀 グルグル開始');
const hideLoadingSpinner = () => console.log('🧹 グルグル消去');
const downloadData = () => new Promise((resolve, reject) => {
    Math.random() > 0.5 ? resolve('成功データ') : reject('通信エラー');
});
const showData = (d) => console.log('✅ ' + d);
const showError = (e) => console.log('❌ ' + e);
```

### 4. D09.md (Promise.all)
- **現状**: `getUser()`, `getFriends()`, `getImportantData()`, `getErrorData()` が未定義です。
- **提案**: 時間短縮効果（3秒+2秒=5秒 vs 3秒）を体感するには、`setTimeout` を使った正確な実装が必要です。

```javascript
// Promise.all 実験用
const getUser = () => new Promise(r => setTimeout(() => r({name:'イチカ'}), 3000));
const getFriends = () => new Promise(r => setTimeout(() => r(['A','B']), 2000));
```

### 5. D12.md (POST)
- **現状**: `https://example.com/api/order` にPOSTするコードがありますが、`example.com` はPOSTを受け付けてJSONを返さないため、そのまま実行すると構文エラー（JSON.parse error）になります。
- **提案**: 「※このコードは例なので動きません。実際に試す場合は下のJSONPlaceholderを使ってね」という注釈を強調するか、ダミーAPIのエンドポイントを `https://jsonplaceholder.typicode.com/posts` に統一する手もあります（ただし、headersの意味を教える文脈ならexample.comのままで注釈が無難かもしれません）。

### 6. D13.md (Abort / 404)
- **現状**: キャンセル実験で `https://slow-api.com/data` という架空のドメインが使われています。
- **提案**: 実際に「遅いAPI」をキャンセルさせたい場合、実在する遅延API（例: `https://httpbin.org/delay/3`）を使うと、リアルなキャンセル挙動を体験できます。

```javascript
// 実際に3秒待たされるURL
const response = await fetch('https://httpbin.org/delay/3', { ... });
```

---

これらを追加することで、学習者が「コピペで即実験」できるようになり、学習効率が向上します。
修正を進めてよろしいでしょうか？
