<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>予約ページ</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: sans-serif;
      margin: 2rem;
    }

    .iframe-container {
      position: relative;
      width: 100%;
      padding-bottom: 75%; /* 高さ比率（4:3相当）を維持 */
      height: 0;
      overflow: hidden;
    }

    .iframe-container iframe {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      border: none;
    }

    h1 {
      font-size: 1.5rem;
      margin-bottom: 1rem;
    }
  </style>
</head>
<body>
  <h1>予約状況</h1>
  <div class="iframe-container">
    <iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSZNTzUfoN7HbKfX-k_ZziFDy9H8OD_LTQSzLjX1CA0r0Of5AjU59ksiAa8bP3ws1TswZb1kWqdomkh/pubhtml?gid=0&amp;single=true&amp;widget=true&amp;headers=false"></iframe>
  </div>
</body>
</html>
