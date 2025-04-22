<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>NOVA-Mini Financial Platform</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet"/>
  <script src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>

  <style>
    :root {
      --primary-bg: #020F1D;
      --accent-blue: #0052CC;
      --text-white: #FFFFFF;
      --secondary-gray: #1B1E27;
      --light-bg: #FFFFFF;
      --light-text: #111111;
      --light-secondary: #F0F0F0;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Inter', sans-serif;
    }

    body {
      background: var(--primary-bg);
      color: var(--text-white);
      transition: background 0.3s, color 0.3s;
    }

    body.light {
      background: var(--light-bg);
      color: var(--light-text);
    }

    .login-container {
      max-width: 400px;
      margin: 100px auto;
      padding: 2rem;
      background: var(--secondary-gray);
      border-radius: 8px;
    }

    body.light .login-container {
      background: var(--light-secondary);
    }

    .input-field {
      width: 100%;
      padding: 12px;
      margin-bottom: 1rem;
      background: var(--primary-bg);
      border: none;
      border-radius: 4px;
      color: white;
    }

    body.light .input-field {
      background: white;
      color: black;
      border: 1px solid #ccc;
    }

    .button {
      width: 100%;
      padding: 12px;
      background: var(--accent-blue);
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-weight: 500;
    }

    .dashboard {
      display: grid;
      grid-template-columns: 250px 1fr;
      min-height: 100vh;
    }

    .sidebar {
      background: var(--primary-bg);
      padding: 2rem 1rem;
      border-right: 1px solid #101820;
    }

    body.light .sidebar {
      background: var(--light-secondary);
    }

    .sidebar h3 {
      margin-bottom: 0.5rem;
    }

    .sidebar p {
      margin-bottom: 2rem;
      font-size: 1.2rem;
      font-weight: bold;
    }

    .nav-button {
      width: 100%;
      padding: 12px;
      margin-bottom: 1rem;
      background: var(--accent-blue);
      border: none;
      border-radius: 4px;
      color: white;
      font-weight: 500;
      cursor: pointer;
    }

    .main-content {
      padding: 2rem;
    }

    .card {
      background: var(--secondary-gray);
      padding: 1.5rem;
      border-radius: 8px;
      margin-bottom: 1rem;
    }

    body.light .card {
      background: var(--light-secondary);
    }

    .theme-toggle {
      margin-top: 1rem;
      padding: 0.5rem 1rem;
      background: transparent;
      color: inherit;
      border: 1px solid;
      border-radius: 4px;
      cursor: pointer;
    }

    @media (max-width: 768px) {
      .dashboard {
        grid-template-columns: 1fr;
      }
      .sidebar {
        border-right: none;
        border-bottom: 1px solid #101820;
      }
    }
  </style>
</head>
<body>
  <div id="root"></div>

  <script type="text/babel">
    function LoginPage({ onLogin }) {
      const [email, setEmail] = React.useState('');
      const [password, setPassword] = React.useState('');

      const handleSubmit = (e) => {
        e.preventDefault();
        if (email && password) {
          onLogin();
        } else {
          alert("Please enter email and password");
        }
      };

      return (
        <div className="login-container">
          <h1 style={{ textAlign: 'center', marginBottom: '2rem' }}>NOVA-Mini</h1>
          <form onSubmit={handleSubmit}>
            <input
              type="email"
              placeholder="Email"
              className="input-field"
              value={email}
              onChange={(e) => setEmail(e.target.value)}
            />
            <input
              type="password"
              placeholder="Password"
              className="input-field"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
            />
            <button type="submit" className="button">Sign In</button>
          </form>
        </div>
      );
    }

    function Dashboard({ onLogout, toggleTheme, isLightMode }) {
      const [btcPrice, setBtcPrice] = React.useState(null);
      const [ethPrice, setEthPrice] = React.useState(null);

      React.useEffect(() => {
        fetch("https://api.coingecko.com/api/v3/simple/price?ids=bitcoin,ethereum&vs_currencies=usd")
          .then(res => res.json())
          .then(data => {
            setBtcPrice(data.bitcoin.usd);
            setEthPrice(data.ethereum.usd);
          });
      }, []);

      return (
        <div className="dashboard">
          <div className="sidebar">
            <h3>Portfolio</h3>
            <p>$25,000.00</p>
            <nav>
              <button className="nav-button">Trading</button>
              <button className="nav-button">Wallet</button>
              <button className="nav-button">Market</button>
              <button className="nav-button" onClick={onLogout}>Logout</button>
              <button className="theme-toggle" onClick={toggleTheme}>
                Switch to {isLightMode ? 'Dark' : 'Light'} Mode
              </button>
            </nav>
          </div>

          <div className="main-content">
            <div className="card">
              <h2>Live Market Prices</h2>
              <p style={{ marginTop: '1rem' }}>Bitcoin: {btcPrice ? `$${btcPrice}` : 'Loading...'}</p>
              <p>Ethereum: {ethPrice ? `$${ethPrice}` : 'Loading...'}</p>
            </div>
            <div className="card">
              <h3>Recent Activity</h3>
              <ul style={{ marginTop: '1rem' }}>
                <li>Buy BTC - $500</li>
                <li>Sell ETH - $300</li>
                <li>Deposit - $1000</li>
              </ul>
            </div>
          </div>
        </div>
      );
    }

    function App() {
      const [loggedIn, setLoggedIn] = React.useState(false);
      const [lightMode, setLightMode] = React.useState(false);

      React.useEffect(() => {
        document.body.className = lightMode ? "light" : "";
      }, [lightMode]);

      return (
        <div>
          {loggedIn ? (
            <Dashboard
              onLogout={() => setLoggedIn(false)}
              toggleTheme={() => setLightMode(!lightMode)}
              isLightMode={lightMode}
            />
          ) : (
            <LoginPage onLogin={() => setLoggedIn(true)} />
          )}
        </div>
      );
    }

    ReactDOM.render(<App />, document.getElementById('root'));
  </script>
</body>
</html>