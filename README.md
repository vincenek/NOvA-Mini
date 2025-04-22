<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>NOvA-Mini</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: #0e0e0e;
      color: #f2f2f2;
      padding: 20px;
    }

    h1 {
      text-align: center;
      color: #00ffc8;
    }

    .wallet-section, .goal-section, .slider-section {
      background-color: #1a1a1a;
      border-radius: 10px;
      padding: 20px;
      margin: 20px 0;
    }

    .wallet-bar {
      background-color: #333;
      height: 30px;
      border-radius: 15px;
      overflow: hidden;
      margin-top: 10px;
    }

    .wallet-fill {
      height: 100%;
      width: 50%;
      background: linear-gradient(90deg, #00ffc8, #007a5e);
      animation: pulse 2s infinite alternate;
    }

    @keyframes pulse {
      from { width: 50%; }
      to { width: 60%; }
    }

    .slider {
      width: 100%;
      margin-top: 10px;
    }

    .goal-progress {
      background-color: #444;
      border-radius: 10px;
      height: 25px;
      margin-top: 10px;
    }

    .goal-fill {
      height: 100%;
      width: 30%;
      background-color: #00ffc8;
      border-radius: 10px;
    }

    label, p {
      margin: 10px 0;
    }
  </style>
</head>
<body>
  <h1>NOvA-Mini: Ghost Wallet</h1>

  <!-- Ghost Wallet Balance Section -->
  <div class="wallet-section">
    <h2>Ghost Wallet</h2>
    <p>Balance: $500</p>
    <div class="wallet-bar">
      <div class="wallet-fill"></div>
    </div>
  </div>

  <!-- Auto Transfer Slider -->
  <div class="slider-section">
    <h2>Auto-Transfer</h2>
    <label for="autoTransfer">% of funds to Ghost Wallet</label>
    <input type="range" id="autoTransfer" class="slider" min="0" max="100" value="10" oninput="updateLabel(this.value)">
    <p id="sliderValue">10%</p>
  </div>

  <!-- Savings Goal Tracker -->
  <div class="goal-section">
    <h2>Savings Goal: New iPad</h2>
    <p>Progress: $150 of $500</p>
    <div class="goal-progress">
      <div class="goal-fill"></div>
    </div>
  </div>

  <script>
    function updateLabel(value) {
      document.getElementById('sliderValue').textContent = value + '%';
    }
  </script>
</body>
</html>