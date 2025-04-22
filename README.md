<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>NOVA-Mini Financial Platform</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
  <!-- React and Babel CDN -->
  <script src="https://unpkg.com/react@17/umd/react.development.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js" crossorigin></script>
  <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
  <style>
    body {
      font-family: 'Inter', sans-serif;
      background-color: #020F1D;
      color: #FFFFFF;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .login-container {
      background-color: #1B1E27;
      padding: 2rem;
      border-radius: 8px;
      width: 300px;
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
  </style>
</head>
<body>
  <div id="root"></div>
  <script type="text/babel">
    function App() {
      const [loggedIn, setLoggedIn] = React.useState(false);
      const [email, setEmail] = React.useState('');
      const [password, setPassword] = React.useState('');

      const handleLogin = (e) => {
        e.preventDefault();
        if (email && password) {
          setLoggedIn(true);
        } else {
          alert("Please enter email and password.");
        }
      };

      if (!loggedIn) {
        return (
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
      } else {
        return (
          <div>
            <h2>Welcome to the Dashboard</h2>
            <p>Your portfolio balance is $25,000.00</p>
            <button onClick={() => setLoggedIn(false)}>Log Out</button>
          </div>
        );
      }
    }

    ReactDOM.render(<App />, document.getElementById('root'));
  </script>
</body>
</html>