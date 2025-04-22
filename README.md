fintech-app/
├── index.html
├── package.json
├── vite.config.js
├── /public
│   └── logo.png
├── /src
│   ├── main.jsx
│   ├── App.jsx
│   ├── /pages
│   │   ├── Login.jsx
│   │   └── Dashboard.jsx
│   ├── /components
│   │   ├── Button.jsx
│   │   ├── InputField.jsx
│   │   └── Card.jsx
│   └── /styles
│       ├── global.css
│       └── variables.css<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" href="/logo.png" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Fintech App</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>{
  "name": "fintech-app",
  "version": "1.0.0",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  },
  "devDependencies": {
    "@vitejs/plugin-react": "^4.0.0",
    "vite": "^4.0.0"
  }
}import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
})import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import './styles/global.css';

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);import React from 'react';
import Login from './pages/Login';
import Dashboard from './pages/Dashboard';

const App = () => {
  const isAuthenticated = false; // mock auth

  return (
    <div>
      {isAuthenticated ? <Dashboard /> : <Login />}
    </div>
  );
};

export default App;import React, { useState } from 'react';
import InputField from '../components/InputField';
import Button from '../components/Button';

const Login = () => {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');

  return (
    <div className="auth-container">
      <img src="/logo.png" alt="Logo" className="logo" />
      <InputField type="email" placeholder="Email" value={email} onChange={(e) => setEmail(e.target.value)} />
      <InputField type="password" placeholder="Password" value={password} onChange={(e) => setPassword(e.target.value)} />
      <Button type="primary" label="Login" onClick={() => alert('Login logic goes here')} />
      <a href="#">Forgot Password?</a>
      <br />
      <a href="#">Sign Up</a>
    </div>
  );
};

export default Login;import React from 'react';
import Card from '../components/Card';

const Dashboard = () => {
  return (
    <div className="dashboard">
      <aside className="sidebar">
        <h2>User Name</h2>
        <nav>
          <a href="#">Dashboard</a>
          <a href="#">Transactions</a>
          <a href="#">Settings</a>
        </nav>
        <button className="logout">Logout</button>
      </aside>
      <main>
        <Card title="Total Balance">$12,345.67</Card>
        <Card title="Recent Transactions">[Table here]</Card>
        <Card title="Market Trends">[Chart here]</Card>
      </main>
    </div>
  );
};

export default Dashboard;import React from 'react';

const Button = ({ type, label, onClick }) => {
  return (
    <button className={`btn ${type}`} onClick={onClick}>
      {label}
    </button>
  );
};

export default Button;import React from 'react';

const InputField = ({ type, placeholder, value, onChange }) => {
  return (
    <input className="input" type={type} placeholder={placeholder} value={value} onChange={onChange} />
  );
};

export default InputField;import React from 'react';

const Card = ({ title, children }) => {
  return (
    <div className="card">
      <h2>{title}</h2>
      <div>{children}</div>
    </div>
  );
};

export default Card;:root {
  --primary-bg: #020F1D;
  --accent: #0052CC;
  --text: #ffffff;
  --secondary-bg: #1B1E27;
  --font: 'Inter', sans-serif;
}@import './variables.css';

body {
  margin: 0;
  background-color: var(--primary-bg);
  color: var(--text);
  font-family: var(--font);
}

input.input {
  background-color: var(--secondary-bg);
  color: var(--text);
  border: none;
  border-radius: 6px;
  padding: 12px;
  margin: 10px 0;
  width: 100%;
}

button.btn.primary {
  background-color: var(--accent);
  color: var(--text);
  border: none;
  padding: 12px;
  font-weight: bold;
  border-radius: 6px;
  width: 100%;
}

.card {
  background-color: var(--secondary-bg);
  padding: 20px;
  margin: 10px;
  border-radius: 8px;
  box-shadow: 0px 4px 12px rgba(0,0,0,0.3);
}

.sidebar {
  width: 250px;
  background-color: var(--primary-bg);
  padding: 20px;
  height: 100vh;
  float: left;
}

main {
  margin-left: 250px;
  padding: 20px;
}