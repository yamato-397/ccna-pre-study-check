# CCNA研修前ミニテスト

CCNA座学予習の理解度確認を目的としたミニテスト集です。  
GitHub Pagesで静的サイトとして公開しています。

> このリポジトリは [`ccna-quiz-public`](https://github.com/yamato-397/ccna-quiz-public) から研修前ミニテストを分離したものです。

---

## 公開URL

| ページ | URL |
|---|---|
| テスト一覧 | https://yamato-397.github.io/ccna-pre-study-check/ |
| 第1回 | https://yamato-397.github.io/ccna-pre-study-check/01/ |
| 第2回 | https://yamato-397.github.io/ccna-pre-study-check/02/ |
| 第3回 | https://yamato-397.github.io/ccna-pre-study-check/03/ |
| 第4回 | https://yamato-397.github.io/ccna-pre-study-check/04/ |

---

## ディレクトリ構成

```
ccna-pre-study-check/
├── index.html              # テスト一覧ページ
├── 01/
│   └── index.html          # 第1回ミニテスト
├── 02/
│   └── index.html          # 第2回ミニテスト
├── 03/
│   └── index.html          # 第3回ミニテスト
├── 04/
│   └── index.html          # 第4回ミニテスト
├── data/
│   ├── pre-study-check-01.json   # 第1回問題データ
│   ├── pre-study-check-02.json   # 第2回問題データ
│   ├── pre-study-check-03.json   # 第3回問題データ
│   └── pre-study-check-04.json   # 第4回問題データ
├── .nojekyll               # GitHub PagesのJekyll処理を無効化
├── .gitignore
└── README.md
```

---

## 新しいテストを追加する方法

### 1. 問題データを作成する

```
data/pre-study-check-05.json
```

形式は既存のJSONに合わせてください。必須フィールド：

```json
{
  "id": "pre-study-05",
  "title": "CCNA 座学予習確認テスト 第5回",
  "questions": [
    {
      "id": "pre-study-05-001",
      "section": "new",
      "sectionLabel": "今回の範囲",
      "question": "問題文",
      "choices": ["A", "B", "C", "D"],
      "correctIndex": 0,
      "explanation": "解説文",
      "sourceReference": "参照箇所"
    }
  ]
}
```

`section` フィールドは `"review"`（復習問題）または `"new"`（今回の新規範囲）を使用してください。

### 2. HTMLページを作成する

`04/index.html` をコピーして `05/index.html` を作成し、先頭のCONFIG部分を変更します：

```js
const JSON_PATH = '../data/pre-study-check-05.json';
```

また、以下の文字列を第4回→第5回に合わせて更新してください：
- タイトルタグ・h1・start-title・start-theme の「第4回」「ACL・DHCP・QoS」
- section-breakdown の「第3回の復習」→「第4回の復習」
- source-box のリンク（今回の新規範囲のURL）
- scoreTest() の breakdownEl.innerHTML 内の「第3回の復習」→「第4回の復習」
- renderDetailList() のフォールバック文字列「第3回の復習」→「第4回の復習」

### 3. 一覧ページにリンクを追加する

`index.html` の `<!-- 第5回以降はここに追加 -->` コメントの前に追加してください。

### 4. コミットしてpush

```bash
git add 05/index.html data/pre-study-check-05.json index.html README.md
git commit -m "add pre-study check test 05"
git push origin main
```

---

## ローカルでの確認方法

```bash
cd ccna-pre-study-check
python3 -m http.server 8000
```

ブラウザで以下を開いてください：

| ページ | URL |
|---|---|
| テスト一覧 | http://localhost:8000/ |
| 第1回 | http://localhost:8000/01/ |
| 第2回 | http://localhost:8000/02/ |

---

## GitHub Pagesの公開方法

1. GitHubでリポジトリを開く
2. **Settings → Pages**
3. **Source**: `Deploy from a branch`
4. **Branch**: `main` / `/(root)`
5. **Save**

---

## 問題内容を編集する際の注意事項

- 問題文・選択肢・正解・解説は `data/pre-study-check-XX.json` を編集してください
- `correctIndex` は 0始まりです（A=0, B=1, C=2, D=3）
- HTMLファイルの採点ロジックや画面デザインは、内容修正でなければ変更不要です
- 問題IDは重複させないようにしてください（例：`pre-study-03-001`）
- 変更後はローカルサーバーで動作確認してからpushしてください
