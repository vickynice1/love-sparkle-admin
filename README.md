<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Love Sparkle Admin</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" />
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #ffe6f0, #ffcce5);
      color: #333;
      overflow-x: hidden;
      animation: fadeInBody 1.2s ease-in-out;
    }

    @keyframes fadeInBody {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    header {
      background: #ff66a3;
      color: #fff;
      padding: 1.5rem;
      text-align: center;
      font-size: 1.8rem;
      font-weight: bold;
      letter-spacing: 1px;
      animation: typing 3s steps(22) 1s 1 normal both;
      white-space: nowrap;
      overflow: hidden;
      border-right: 3px solid #fff;
    }

    @keyframes typing {
      from { width: 0; }
      to { width: 100%; }
    }

    .panel {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
      gap: 15px;
      padding: 20px;
      animation: fadeIn 1.5s ease-in;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    button {
      background: #ff3385;
      border: none;
      color: white;
      padding: 15px;
      border-radius: 12px;
      font-size: 15px;
      cursor: pointer;
      transition: 0.3s ease-in-out;
      box-shadow: 0 6px 10px rgba(0,0,0,0.1);
    }

    button:hover {
      transform: scale(1.05);
      background: #e60073;
    }

    .form-section {
      padding: 20px;
      animation: fadeInUp 1.8s ease;
    }

    @keyframes fadeInUp {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    h3 {
      color: #cc0066;
    }

    input, select {
      width: 100%;
      padding: 12px;
      margin-top: 10px;
      margin-bottom: 20px;
      border: 1px solid #ccc;
      border-radius: 10px;
      font-size: 14px;
    }

    .footer {
      text-align: center;
      padding: 1rem;
      font-size: 0.9rem;
      color: #888;
      background: #fff0f5;
      margin-top: 20px;
    }

    @media screen and (max-width: 500px) {
      header {
        font-size: 1.4rem;
      }

      .panel {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>
<body>
  <header>👑 Love Sparkle Admin Panel</header>

  <div class="panel">
    <button onclick="runCommand('view_users')">👥 View Users</button>
    <button onclick="runCommand('view_matches')">💌 View Matches</button>
    <button onclick="runCommand('view_reports')">🚨 View Reports</button>
    <button onclick="runCommand('manual_match')">💬 Manual Match</button>
    <button onclick="runCommand('search_user')">🔎 Search User</button>
    <button onclick="runCommand('ban_user')">🔒 Ban User</button>
  </div>

  <div class="form-section">
    <h3>⭐ Add Stars</h3>
    <input type="text" id="star_user_id" placeholder="Enter Telegram ID">
    <input type="number" id="star_amount" placeholder="Amount of Stars">
    <button onclick="addStars()">➕ Add Stars</button>

    <h3>👑 Upgrade to Premium</h3>
    <input type="text" id="premium_user_id" placeholder="Enter Telegram ID">
    <button onclick="upgradeUser()">🚀 Upgrade</button>
  </div>

  <div class="footer">© 2025 Love Sparkle Bot</div>

  <script>
    const tg = window.Telegram.WebApp;
    tg.expand();

    function runCommand(command) {
      tg.sendData(JSON.stringify({ action: command }));
    }

    function addStars() {
      const userId = document.getElementById("star_user_id").value.trim();
      const amount = document.getElementById("star_amount").value.trim();

      if (!userId || !amount) {
        alert("Please enter Telegram ID and star amount.");
        return;
      }

      tg.sendData(JSON.stringify({
        action: "add_stars",
        user_id: userId,
        amount: amount
      }));
    }

    function upgradeUser() {
      const userId = document.getElementById("premium_user_id").value.trim();

      if (!userId) {
        alert("Please enter Telegram ID.");
        return;
      }

      tg.sendData(JSON.stringify({
        action: "upgrade_user",
        user_id: userId
      }));
    }
  </script>
</body>
</html>
