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
    
  .responsive-iframe-wrapper {
    width: 100%;
    overflow-x: auto;
  }

  .responsive-iframe-container {
    width: 1200px; /* 固定幅でスプレッドシートの全列を表示 */
    height: 800px;
    border-radius: 12px;
    box-shadow: 0 0 10px rgba(0,0,0,0.2);
    margin: 0 auto;
  }

  .responsive-iframe-container iframe {
    width: 100%;
    height: 100%;
    border: 0;
  }

  @media (max-width: 600px) {
    .responsive-iframe-container {
      width: 1000px; /* スマホ用でも横に広く保つ */
      height: 900px;
    }
  }

  .form-container {
    width: 100%;
    max-width: 1200px;
    margin: 40px auto;
    padding: 30px;
    background: #f9f9f9;
    border-radius: 16px;
    box-shadow: 0 0 15px rgba(0,0,0,0.1);
    box-sizing: border-box;
  }

  .form-container h2 {
    margin-bottom: 24px;
    font-size: 28px;
    text-align: center;
  }

  .form-group {
    margin-bottom: 20px;
    display: flex;
    flex-direction: column;
  }

  .form-group label {
    margin-bottom: 6px;
    font-weight: bold;
    font-size: 16px;
  }

  .form-group input,
  .form-group textarea,
  .form-group select {
    padding: 12px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 8px;
    width: 100%;
    box-sizing: border-box;
  }

  .form-group textarea {
    resize: vertical;
  }

  .form-submit {
    text-align: center;
    margin-top: 25px;
  }

  .form-submit button {
    background-color: #007bff;
    color: white;
    padding: 14px 28px;
    font-size: 16px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
  }

  .form-submit button:hover {
    background-color: #0056b3;
  }

  @media (max-width: 768px) {
    .form-container {
      padding: 20px;
    }

    .form-group label {
      font-size: 15px;
    }

    .form-group input,
    .form-group textarea,
    .form-group select {
      font-size: 15px;
    }

    .form-submit button {
      font-size: 15px;
      padding: 12px 24px;
    }
  }
  
  </style>
</head>
<body>

<div class="responsive-iframe-container">

<iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSZNTzUfoN7HbKfX-k_ZziFDy9H8OD_LTQSzLjX1CA0r0Of5AjU59ksiAa8bP3ws1TswZb1kWqdomkh/pubhtml?gid=0&amp;single=true&amp;widget=true&amp;headers=false"></iframe>

</div>
  

<div class="form-container">
  <h2>予約フォーム</h2>
  <form id="bookingForm">
    <div class="form-group">
      <label for="name">お名前</label>
      <input type="text" id="name" name="name" required />
    </div>

    <div class="form-group">
      <label for="email">メールアドレス</label>
      <input type="email" id="email" name="email" required />
    </div>

    <div class="form-group">
      <label for="pickup">発送元（住所や施設名）</label>
      <input type="text" id="pickup" name="pickup" required />
    </div>

    <div class="form-group">
      <label for="destination">発送先</label>
      <input type="text" id="destination" name="destination" required />
    </div>

    <div class="form-group">
      <label for="delivery_method">受け渡し方法</label>
      <select id="delivery_method" name="delivery_method" required>
        <option value="">選択してください</option>
        <option value="対面で受け渡し">対面で受け渡し</option>
        <option value="玄関前に置く">玄関前に置く</option>
        <option value="宅配業者を使用">宅配業者を使用</option>
      </select>
    </div>

    <div class="form-group">
      <label for="date">発送希望日</label>
      <input type="date" id="date" name="date" required />
    </div>

    <div class="form-group">
      <label for="message">ご要望・メモ</label>
      <textarea id="message" name="message" rows="4"></textarea>
    </div>

    <div class="form-submit">
      <button type="submit">予約する</button>
    </div>
  </form>
</div>

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
