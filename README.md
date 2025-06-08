<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>予約フォーム</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0 16px;
      background-color: #f5f5f5;
    }

    .check-link {
      text-align: center;
      margin: 30px 0 10px;
    }

    .check-link a {
      font-size: 18px;
      text-decoration: underline;
      color: #007bff;
      cursor: pointer;
    }

    .iframe-wrapper {
      display: none;
      margin: 20px auto;
      max-width: 1200px;
    }

    .iframe-wrapper iframe {
      width: 100%;
      height: 600px;
      border: none;
      border-radius: 12px;
      box-shadow: 0 0 10px rgba(0,0,0,0.2);
    }

    .form-container {
      width: 100%;
      max-width: 1200px;
      margin: 30px auto;
      padding: 30px;
      background: #fff;
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
      .form-group label,
      .form-group input,
      .form-group textarea,
      .form-group select,
      .form-submit button {
        font-size: 15px;
      }
    }
  </style>
</head>
<body>

  <!-- 空き状況チェックリンク -->
  <div class="check-link">
    <a onclick="toggleIframe()">▶ 空き状況をチェック</a>
  </div>

  <!-- 非表示 iframe -->
  <div class="iframe-wrapper" id="availabilityIframe">
    <iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSZNTzUfoN7HbKfX-k_ZziFDy9H8OD_LTQSzLjX1CA0r0Of5AjU59ksiAa8bP3ws1TswZb1kWqdomkh/pubhtml?gid=0&amp;single=true&amp;widget=true&amp;headers=false" allowfullscreen></iframe>
  </div>

  <!-- 予約フォーム -->
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
        <label for="pickup">発送元</label>
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
          <option value="その他指定の場所　※要望欄に記入をお願いいたします">玄関前に置く</option>
        </select>
      </div>

      <div class="form-group">
        <label for="date">引取希望日</label>
        <input type="date" id="date" name="date" required />
      </div>

      <div class="form-group">
        <label for="date">到着希望日</label>
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

  <!-- スクリプト -->
  <script>
    function toggleIframe() {
      const iframe = document.getElementById("availabilityIframe");
      iframe.style.display = iframe.style.display === "none" ? "block" : "none";
    }
  </script>

</body>
</html>
