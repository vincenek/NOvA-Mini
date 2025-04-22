<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NOVA-Mini Financial Platform</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
    <!-- React and Babel CDN -->
    <script src="https://unpkg.com/react@17/umd/react.development.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js" crossorigin></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
    <style>
        /* Global Styles */
        body {
            font-family: 'Inter', sans-serif;
            background-color: #020F1D;
            color: #FFFFFF;
            margin: 0;
            padding: 0;
            display: flex;
            height: 100vh;
            flex-direction: column;
        }

        /* Container and Login Form */
        .login-container {
            background-color: #1B1E27;
            padding: 2rem;
            border-radius: 8px;
            width: 350px;
            margin: auto;
            margin-top: 10%;
        }

        .login-container h2 {
            text-align: center;
            margin-bottom: 1rem;
        }

        input, button {
            width: 100%;
            padding: 0.5rem;
            margin-top: 1rem;
            border: none;
            border-radius: 4px;
        }

        button {
            background-color: #0052CC;
            color: #FFFFFF;
            cursor: pointer;
        }

        /* Sidebar Styles */
        .sidebar {
            background-color: #020F1D;
            padding: 2rem;
            min-width: 200px;
            height: 100vh;
        }

        .sidebar h3 {
            color: #0052CC;
            margin-bottom: 2rem;
        }

        .sidebar button {
            background-color: #0052CC;
            color: #FFFFFF;
            width: 100%;
            padding: 12px;
            margin-bottom: 1rem;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }

        /* Dashboard Styles */
        .dashboard {
            display: flex;
        }

        .dashboard-content {
            flex-grow: 1;
            padding: 2rem;
            background-color: #1B1E27;
        }

        .card {
            background-color: #2E333A;
            padding: 1rem;
            margin: 1rem 0;
            border-radius: 8px;
        }

        .card h4 {
            margin-bottom: 0.5rem;
        }

        .card p {
            font-size: 1.2rem;
        }

        /* Navbar Styles */
        .navbar {
            background-color: #020F1D;
            color: #ffffff;
            padding: 1rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .navbar h1 {
            font-size: 1.5rem;
        }

        .navbar .logout {
            background-color: #d9534f;
            padding: 0.5rem 1rem;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        // Simulating Financial Platform App with Login and Dashboard
        function App() {
            const [loggedIn, setLoggedIn] = React.useState(false);
            const [email, setEmail] = React.useState('');
            const [password, setPassword] = React.useState('');
            const [showDashboard, setShowDashboard] = React.useState(true);
            const [portfolioValue, setPortfolioValue] = React.useState(25000);
            const [transactionHistory, setTransactionHistory] = React.useState([
                { id: 1, type: 'Deposit', amount: 5000 },
                { id: 2, type: 'Withdrawal', amount: 2000 },
                { id: 3, type: 'Transfer', amount: 1500 }
            ]);

            // Handle Login
            const handleLogin = (e) => {
                e.preventDefault();
                if (email && password) {
                    setLoggedIn(true);
                } else {
                    alert("Please enter email and password.");
                }
            };

            // Handle Logout
            const handleLogout = () => {
                setLoggedIn(false);
                setEmail('');
                setPassword('');
            };

            // Dashboard Components
            const Dashboard = () => (
                <div>
                    <div className="navbar">
                        <h1>NOVA-Mini</h1>
                        <button className="logout" onClick={handleLogout}>Log Out</button>
                    </div>

                    <div className="dashboard">
                        <div className="sidebar">
                            <h3>Portfolio</h3>
                            <p>${portfolioValue}</p>
                            <button onClick={() => alert('Show Transactions')}>Transactions</button>
                            <button onClick={() => alert('Show Settings')}>Settings</button>
                        </div>

                        <div className="dashboard-content">
                            <h2>Dashboard</h2>
                            <div className="card">
                                <h4>Market Overview</h4>
                                <p>Current Balance: ${portfolioValue}</p>
                            </div>
                            <div className="card">
                                <h4>Recent Transactions</h4>
                                <ul>
                                    {transactionHistory.map(transaction => (
                                        <li key={transaction.id}>{transaction.type}: ${transaction.amount}</li>
                                    ))}
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
            );

            // Login Form Component
            const LoginPage = () => (
                <div className="login-container">
                    <h2>NOVA-Mini</h2>
                    <form onSubmit={handleLogin}>
                        <input
                            type="email"
                            placeholder="Email"
                            value={email}
                            onChange={(e) => setEmail(e.target.value)}
                        />
                        <input
                            type="password"
                            placeholder="Password"
                            value={password}
                            onChange={(e) => setPassword(e.target.value)}
                        />
                        <button type="submit">Sign In</button>
                    </form>
                </div>
            );

            return (
                <div>
                    {!loggedIn ? <LoginPage /> : <Dashboard />}
                </div>
            );
        }

        ReactDOM.render(<App />, document.getElementById('root'));
    </script>
</body>
</html>