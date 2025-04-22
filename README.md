<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NOvA-X Dashboard</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="dashboard-container">
        <div class="sidebar">
            <div class="user-profile">
                <img src="avatar.png" alt="User Avatar">
                <h3>User Name</h3>
                <p>Active</p>
            </div>
            <nav>
                <ul>
                    <li><a href="#">Dashboard</a></li>
                    <li><a href="#">Transactions</a></li>
                    <li><a href="#">Settings</a></li>
                    <li><a href="#">Logout</a></li>
                </ul>
            </nav>
        </div>
        <div class="main-content">
            <div class="top-nav">
                <div class="search-bar">
                    <input type="text" placeholder="Search">
                </div>
                <div class="notification">
                    <img src="bell.png" alt="Notifications">
                </div>
                <div class="user-dropdown">
                    <img src="avatar.png" alt="User Avatar">
                </div>
            </div>
            <div class="content-body">
                <div class="balance-card">
                    <h2>Total Balance</h2>
                    <p>$10,000.00</p>
                </div>
                <div class="transactions">
                    <h3>Recent Transactions</h3>
                    <table>
                        <tr>
                            <th>Date</th>
                            <th>Amount</th>
                            <th>Status</th>
                        </tr>
                        <tr>
                            <td>2025-04-22</td>
                            <td>$200.00</td>
                            <td>Completed</td>
                        </tr>
                        <tr>
                            <td>2025-04-21</td>
                            <td>$500.00</td>
                            <td>Pending</td>
                        </tr>
                    </table>
                </div>
                <div class="market-trends">
                    <h3>Market Trends</h3>
                    <div class="chart-container">
                        <!-- Placeholder for chart (You can later replace it with a real chart) -->
                        <div class="chart">Chart goes here</div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <script src="script.js"></script>
</body>
</html>body {
    margin: 0;
    font-family: 'Inter', sans-serif;
    background-color: #020F1D;
    color: white;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    height: 100vh;
}

.dashboard-container {
    display: flex;
    width: 100%;
}

.sidebar {
    background-color: #1B1E27;
    width: 250px;
    padding: 20px;
}

.sidebar .user-profile {
    text-align: center;
}

.sidebar nav ul {
    list-style-type: none;
    padding: 0;
}

.sidebar nav ul li {
    margin: 15px 0;
}

.sidebar nav ul li a {
    color: white;
    text-decoration: none;
    font-size: 16px;
}

.main-content {
    flex-grow: 1;
    padding: 20px;
}

.top-nav {
    display: flex;
    justify-content: space-between;
    padding: 10px 0;
    border-bottom: 1px solid #3A3A3A;
}

.top-nav .search-bar input {
    padding: 5px;
    border-radius: 6px;
    border: 1px solid #3A3A3A;
    background-color: #1B1E27;
    color: white;
}

.top-nav .notification img {
    width: 20px;
}

.top-nav .user-dropdown img {
    width: 30px;
    border-radius: 50%;
}

.content-body {
    margin-top: 20px;
}

.balance-card {
    background-color: #1B1E27;
    padding: 20px;
    margin-bottom: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 20px rgba(0, 82, 204, 0.4);
}

.transactions table {
    width: 100%;
    border-collapse: collapse;
}

.transactions table th, .transactions table td {
    padding: 10px;
    border: 1px solid #3A3A3A;
}

.chart-container {
    margin-top: 20px;
    background-color: #1B1E27;
    padding: 20px;
    border-radius: 8px;
    height: 200px;
}

.chart {
    background-color: #0052CC;
    height: 100%;
    text-align: center;
    line-height: 200px;
    color: white;
}function login() {
    const email = document.getElementById("email").value;
    const password = document.getElementById("password").value;

    if (email && password) {
        alert("Welcome to NOvA-X, " + email + "!");
    } else {
        alert("Please enter both email and password.");
    }
}