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

    .section {
      background-color: #1a1a1a;
      border-radius: 10px;
      padding: 20px;
      margin: 20px 0;
    }

    input, button {
      padding: 10px;
      margin: 5px 0;
      border-radius: 5px;
      border: none;
      width: 100%;
    }

    button {
      background-color: #00ffc8;
      color: #000;
      font-weight: bold;
      cursor: pointer;
    }

    .wallet-bar, .goal-progress {
      background-color: #333;
      border-radius: 15px;
      overflow: hidden;
      height: 30px;
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

    ul {
      list-style-type: none;
      padding: 0;
    }

    li {
      background: #2a2a2a;
      margin: 5px 0;
      padding: 8px;
      border-radius: 5px;
    }
  </style>
</head>
<body>

  <h1>NOvA-Mini: Ghost Wallet Prototype</h1>

  <!-- Ghost Wallet Balance -->
  <div class="section">
    <h2>Ghost Wallet</h2>
    <p id="ghostBalance">$0</p>
    <div class="wallet-bar">
      <div class="wallet-fill" id="walletFill"></div>
    </div>
  </div>

  <!-- Savings Calculator -->
  <div class="section">
    <h2>Savings Calculator</h2>
    <label>Monthly Income ($)</label>
    <input type="number" id="incomeInput" placeholder="Enter your income">
    <label>Save (%)</label>
    <input type="number" id="saveInput" placeholder="e.g. 20">
    <button onclick="calculateSavings()">Calculate</button>
    <p id="saveResult"></p>
    <p id="spendResult"></p>
  </div>

  <!-- Expense Tracker -->
  <div class="section">
    <h2>Expense Tracker</h2>
    <input type="number" id="expenseAmount" placeholder="Amount ($)">
    <input type="text" id="expenseNote" placeholder="Note (e.g. Food)">
    <button onclick="addExpense()">Add Expense</button>
    <ul id="expenseList"></ul>
    <p id="expenseTotal"></p>
  </div>

  <script>
    let ghostBalance = 0;
    let totalExpenses = 0;

    function calculateSavings() {
      const income = parseFloat(document.getElementById('incomeInput').value);
      const percent = parseFloat(document.getElementById('saveInput').value);

      if (isNaN(income) || isNaN(percent)) {
        alert("Please enter valid numbers.");
        return;
      }

      const saved = (income * percent / 100).toFixed(2);
      const spend = (income - saved).toFixed(2);

      ghostBalance = parseFloat(saved);
      document.getElementById('ghostBalance').textContent = `$${saved}`;
      document.getElementById('walletFill').style.width = Math.min(percent, 100) + '%';

      document.getElementById('saveResult').textContent = `Saved: $${saved}`;
      document.getElementById('spendResult').textContent = `Left to Spend: $${spend}`;
    }

    function addExpense() {
      const amount = parseFloat(document.getElementById('expenseAmount').value);
      const note = document.getElementById('expenseNote').value.trim();

      if (isNaN(amount) || note === "") {
        alert("Please enter a valid amount and note.");
        return;
      }

      totalExpenses += amount;

      const li = document.createElement('li');
      li.textContent = `$${amount.toFixed(2)} - ${note}`;
      document.getElementById('expenseList').appendChild(li);

      document.getElementById('expenseTotal').textContent = `Total Spent: $${totalExpenses.toFixed(2)}`;
      
      document.getElementById('expenseAmount').value = "";
      document.getElementById('expenseNote').value = "";
    }
  </script>

</body>
</html>