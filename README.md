<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
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

        .dashboard {
            display: grid;
            grid-template-columns: 250px 1fr;
            min-height: 100vh;
        }
    </style>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        function LoginPage() {
            return (
                <div className="login-container">
                    <h1 style={{textAlign: 'center', marginBottom: '2rem'}}>NOVA-Mini</h1>
                    <form>
                        <input 
                            type="email"
                            placeholder="Email"
                            style={{
                                width: '100%',
                                padding: '12px',
                                marginBottom: '1rem',
                                background: var(--primary-bg),
                                border: 'none',
                                borderRadius: '4px',
                                color: 'white'
                            }}
                        />
                        <input 
                            type="password"
                            placeholder="Password"
                            style={{
                                width: '100%',
                                padding: '12px',
                                marginBottom: '1rem',
                                background: var(--primary-bg),
                                border: 'none',
                                borderRadius: '4px',
                                color: 'white'
                            }}
                        />
                        <button 
                            style={{
                                width: '100%',
                                padding: '12px',
                                background: var(--accent-blue),
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

        function Dashboard() {
            return (
                <div className="dashboard">
                    {/* Sidebar */}
                    <div style={{
                        background: var(--primary-bg),
                        padding: '1rem'
                    }}>
                        <h3>Portfolio</h3>
                        <p>$25,000.00</p>
                        <nav style={{marginTop: '2rem'}}>
                            <button style={{
                                width: '100%',
                                padding: '12px',
                                margin: '8px 0',
                                background: var(--accent-blue),
                                border: 'none',
                                borderRadius: '4px',
                                color: 'white',
                                cursor: 'pointer'
                            }}>
                                Trading
                            </button>
                        </nav>
                    </div>

                    {/* Main Content */}
                    <div style={{padding: '2rem'}}>
                        <div style={{
                            background: var(--secondary-gray),
                            padding: '1rem',
                            borderRadius: '8px',
                            marginBottom: '1rem'
                        }}>
                            <h2>Market Overview</h2>
                            <div id="chart" style={{height: '300px', marginTop: '1rem'}}></div>
                        </div>
                    </div>
                </div>
            );
        }

        function App() {
            const [loggedIn, setLoggedIn] = React.useState(false);

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