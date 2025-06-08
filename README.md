<html lang="ja">
<head>
  <meta charset="UTF-8" />
  <title>予約フォーム</title>
  <style>
    body { font-family: Arial, sans-serif; background: #f0f0f0; padding: 30px; }
    form { background: #fff; padding: 20px; border-radius: 8px; max-width: 400px; margin: auto; }
    label { display: block; margin-top: 10px; font-weight: bold; }
    input, textarea { width: 100%; padding: 8px; margin-top: 4px; border-radius: 4px; border: 1px solid #ccc; }
    button { margin-top: 20px; padding: 10px 15px; background: #4caf50; color: white; border: none; border-radius: 4px; cursor: pointer; }
    button:hover { background: #45a049; }
    #status { margin-top: 15px; font-weight: bold; }
    
  .responsive-iframe-container {
    position: relative;
    width: 100%;
    padding-top: 70%; /* 高さ比率（必要に応じて調整） */
    overflow: hidden;
    border-radius: 12px;
    box-shadow: 0 0 10px rgba(0,0,0,0.2);
    margin: 20px auto;
    max-width: 1200px;
  }

  .responsive-iframe-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border: 0;
  }

  @media (max-width: 600px) {
    .responsive-iframe-container {
      padding-top: 120%; /* スマホは縦長に調整 */
    }
  }

  </style>
</head>
<body>

<iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSZNTzUfoN7HbKfX-k_ZziFDy9H8OD_LTQSzLjX1CA0r0Of5AjU59ksiAa8bP3ws1TswZb1kWqdomkh/pubhtml?gid=0&amp;single=true&amp;widget=true&amp;headers=false"></iframe>
  
  <form id="reservationForm">
    <label for="name">お名前</label>
    <input type="text" id="name" name="name" required />

    <label for="date">予約日</label>
    <input type="date" id="date" name="date" required />

    <label for="from">発送元住所</label>
    <input type="text" id="from" name="from" required />

    <label for="to">発送先住所</label>
    <input type="text" id="to" name="to" required />

    <label for="message">備考・メッセージ</label>
    <textarea id="message" name="message" rows="4"></textarea>

    <button type="submit">送信</button>
    <div id="status"></div>
  </form>

  <script>
    const GAS_WEBAPP_URL = 'YOUR_GAS_DEPLOY_URL'; // ①で控えたWebアプリURLをここに貼る

    document.getElementById('reservationForm').addEventListener('submit', async (e) => {
      e.preventDefault();
      const status = document.getElementById('status');
      status.textContent = '送信中…';

      const data = {
        name: e.target.name.value,
        date: e.target.date.value,
        message: e.target.message.value,
      };

      try {
        const res = await fetch(GAS_WEBAPP_URL, {
          method: 'POST',
          body: JSON.stringify(data),
          headers: {
            'Content-Type': 'application/json'
          }
        });

        const result = await res.json();
        if (result.status === 'success') {
          status.textContent = '予約が送信されました！LINEに通知済みです。';
          e.target.reset();
        } else {
          status.textContent = '送信に失敗しました: ' + (result.message || '不明なエラー');
        }
      } catch (err) {
        status.textContent = '通信エラーが発生しました。';
        console.error(err);
      }
    });
  </script>
</body>
</html>
