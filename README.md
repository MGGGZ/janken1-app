# webpro_06
10/29

## このプログラムについて
## ファイル一覧

ファイル名 | 説明
-|-
app5.js | プログラム本体
public/janken.html | じゃんけんの開始画面
views/gacha.ejs|gachaテンプレートのエンジン
views/quiz.ejs|quizテンプレートのエンジン

## 追加したプログラミング

### ガチャでよくある１回と１０回を選べる

```javascript
app.get("/gacha", (req, res) => {
  const pulls = Number(req.query.pulls) || 0; 
  const results = [];

  if (pulls > 0) {
    for (let i = 0; i < pulls; i++) {
      const randomNum = Math.random();
      let result;

      if (randomNum < 0.05) {
        result = '白銀王者ライオウ';
      } else if (randomNum < 0.20) {
        result = '黄金王者エレファ';
      } else if (randomNum < 0.50) {
        result = '銅獣王者ハイーナ';
      
      } else {
        result = '郡獣王者ガーゼル';
      }

      results.push(result); 
    }
  }

  res.render('gacha', { results });
});
```
/gachaは,webでアクセスするとこの関数が実行される。
(req.query.pulls)は追加データとして扱い、条件選択で指定された分ガチャを回し、その結果を表示させる。
初期状態では、値は0であるため何も表示されません。
const results = [];はガチャの結果を保存する配列。
if (pulls > 0)はpullsが0よりも大きい場合はにガチャ処理を実行する。
ガチャの確率判定

確率(%)|名称('')
-|-
5%|'白銀王者ライオウ'
15%|'黄金王者エレファ'
30%|'銅獣王者ハイーナ'
50%|'郡獣王者ガーゼル'

```ejs
<!DOCTYPE html>
<html>
<head>
  <title>野蛮猛獣</title>
</head>
<body>
  <h1>野蛮猛獣</h1>

  <% if (results.length > 0) { %>
    <ul>
      <% results.forEach(result => { %>
        <li><%= result %></li>
      <% }); %>
    </ul>
  <% } else { %>

  <% } %>

  <form action="/gacha" method="get">
    <button type="submit" name="pulls" value="1">1回実行</button>
    <button type="submit" name="pulls" value="10">10回実行</button>
  </form>
</body>
</html>

```



```mermaid
flowchart TD;
start["開始"];
end1["終了"]
if{"条件の選択"}
1["1回実行"]
10["10回実行"]

start --> if
if --> 1
1 --> end1
if --> 10
10 --> end1

```

"http://localhost:8080/gacha"をwebで実行すると



