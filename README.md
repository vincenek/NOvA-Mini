<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Budget Breakdown</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      margin: 0;
      padding: 20px;
      background: #f4f6f8;
      color: #333;
    }
    .container {
      max-width: 400px;
      margin: auto;
      background: white;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    h1 {
      text-align: center;
      margin-bottom: 20px;
      color: #1a73e8;
    }
    label {
      display: block;
      margin: 10px 0 5px;
    }
    input {
      width: 100%;
      padding: 10px;
      margin-bottom: 15px;
      box-sizing: border-box;
    }
    button {
      width: 100%;
      padding: 12px;
      background-color: #1a73e8;
      color: white;
      border: none;
      font-size: 16px;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #0c59c1;
    }
    .output {
      margin-top: 20px;
      padding: 15px;
      background: #e8f0fe;
      border-radius: 5px;
    }
    .highlight {
      font-weight: bold;
      color: #0c59c1;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Budget Breakdown</h1>
    <label for="monthlyIncome">Monthly Budget ($)</label>
    <input type="number" id="monthlyIncome" placeholder="Enter your budget" />

    <label for="savings">Savings Goal (%)</label>
    <input type="number" id="savings" placeholder="e.g. 10 for 10%" />

    <button onclick="calculateBudget()">Calculate</button>

    <div id="results" class="output" style="display: none;">
      <p>After savings: <span id="netBudget" class="highlight"></span></p>
      <p>Weekly Budget: <span id="weeklyBudget" class="highlight"></span></p>
      <p>Daily Budget: <span id="dailyBudget" class="highlight"></span></p>
    </div>
  </div>

  <script>
    function calculateBudget() {
      const monthlyIncome = parseFloat(document.getElementById('monthlyIncome').value);
      const savingsPercent = parseFloat(document.getElementById('savings').value) || 0;

      if (!monthlyIncome || monthlyIncome <= 0) {
        alert("Please enter a valid monthly budget.");
        return;
      }

      const savingsAmount = (monthlyIncome * savingsPercent) / 100;
      const netBudget = monthlyIncome - savingsAmount;

      const weeklyBudget = (netBudget / 4).toFixed(2);
      const dailyBudget = (netBudget / 30).toFixed(2);

      document.getElementById('netBudget').textContent = `$${netBudget.toFixed(2)}`;
      document.getElementById('weeklyBudget').textContent = `$${weeklyBudget}`;
      document.getElementById('dailyBudget').textContent = `$${dailyBudget}`;
      document.getElementById('results').style.display = 'block';

      // Optional: Save in local storage
      localStorage.setItem('lastBudget', JSON.stringify({
        monthlyIncome, savingsPercent
      }));
    }

    // Load saved data
    window.onload = function() {
      const saved = JSON.parse(localStorage.getItem('lastBudget'));
      if (saved) {
        document.getElementById('monthlyIncome').value = saved.monthlyIncome;
        document.getElementById('savings').value = saved.savingsPercent;
        calculateBudget();
      }
    };
  </script>
</body>
</html>