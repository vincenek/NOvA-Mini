<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>NOVA-Mini Financial Platform</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
  <script src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
  <style>
    :root {
      --primary-bg: #020F1D;
      --accent-blue: #0052CC;
      --text-white: #FFFFFF;
      --secondary-gray: #1B1E27;
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
    }

    .login-container {
      max-width: 400px;
      margin: 100px auto;
      padding: 2rem;
      background: var(--secondary-gray);
      border-radius: 8px;
    }

    input, button {
      outline: none;
    }

    .dashboard {
      display: grid;
      grid-template-columns: 250px 1fr;
      min-height: 100vh;
    }

    .sidebar {
      background: var(--primary-bg);
      padding: 1rem;
      border-right: 1px solid #333;
    }

    .main-content {
      padding: 2rem;
    }

    .card {
      background: var(--secondary-gray);
      padding: 1rem;
      border-radius: 8px;
      margin-bottom: 1rem;
    }

    .nav-btn {
      width: 100%;
      padding: 12px;
      margin: 8px 0;
      background: var(--accent-blue);
      border: none;
      border-radius: 4px;
      color: white;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div id="root"></div>

  <script type="text/babel">
    function LoginPage({ onLogin }) {
      const [email, setEmail] = React.useState('');
      const [password, setPassword] = React.useState('');

      function handleSubmit(e) {
        e.preventDefault();
        if (email && password) {
          onLogin(); // mock login
        } else {
          alert("Please enter email and password.");
        }
      }

      return (
        <div className="login-container">
          <h1 style={{ textAlign: 'center', marginBottom: '2rem' }}>NOVA-Mini</h1>
          <form onSubmit={handleSubmit}>
            <input
              type="email"
              placeholder="Email"
              value={email}
              onChange={e => setEmail(e.target.value)}
              style={{
                width: '100%',
                padding: '12px',
                marginBottom: '1rem',
                background: 'var(--primary-bg)',
                border: '1px solid #333',
                borderRadius: '4px',
                color: 'white'
              }}
            />
            <input
              type="password"
              placeholder="Password"
              value={password}
              onChange={e => setPassword(e.target.value)}
              style={{
                width: '100%',
                padding: '12px',
                marginBottom: '1rem',
                background: 'var(--primary-bg)',
                border: '1px solid #333',
                borderRadius: '4px',
                color: 'white'
              }}
            />
            <button
              type="submit"
              style={{
                width: '100%',
                padding: '12px',
                background: 'var(--accent-blue)',
                color: 'white',
                border: 'none',
                borderRadius: '4px',
                cursor: 'pointer'
              }}
            >
              Sign In
            </button>
          </form>
        </div>
      );
    }

    function Dashboard({ onLogout }) {
      return (
        <div className="dashboard">
          <div className="sidebar">
            <h3>Portfolio</h3>
            <p>$25,000.00</p>
            <nav style={{ marginTop: '2rem' }}>
              <button className="nav-btn">Trading</button>
              <button className="nav-btn" onClick={onLogout}>Log Out</button>
            </nav>
          </div>
          <div className="main-content">
            <div className="card">
              <h2>Market Overview</h2>
              <div style={{ height: '300px', marginTop: '1rem', background: '#00000044', borderRadius: '8px', display: 'flex', alignItems: 'center', justifyContent: 'center' }}>
                <p>Chart will appear here (future update)</p>
              </div>
            </div>
            <div className="card">
              <h2>Quick Actions</h2>
              <button className="nav-btn">Buy BTC</button>
              <button className="nav-btn">Sell ETH</button>
            </div>
          </div>
        </div>
      );
    }

    function App() {
      const [loggedIn, setLoggedIn] = React.useState(false);

      return (
        <div>
          {!loggedIn ? (
            <LoginPage onLogin={() => setLoggedIn(true)} />
          ) : (
            <Dashboard onLogout={() => setLoggedIn(false)} />
          )}
        </div>
      );
    }

    ReactDOM.render(<App />, document.getElementById('root'));
  </script>
</body>
</html>