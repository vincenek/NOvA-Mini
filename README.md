<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>NOvA-X Financial Platform</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
  <script src="https://unpkg.com/styled-components@5/dist/styled-components.min.js"></script>
  <script src="https://unpkg.com/react-router-dom@6/dist/react-router-dom.development.js"></script>
  <script src="https://unpkg.com/apexcharts"></script>

  <style>
    :root {
      --primary-bg: #020F1D;
      --accent-blue: #0052CC;
      --text-white: #FFFFFF;
      --secondary-gray: #1B1E27;
      --font-inter: 'Inter', sans-serif;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: var(--font-inter);
      background: var(--primary-bg);
      color: var(--text-white);
    }

    .table-row:nth-child(even) {
      background: var(--secondary-gray);
    }
  </style>
</head>
<body>
  <div id="root"></div>

  <script type="text/babel">
    const { BrowserRouter, Routes, Route, Link, useNavigate } = ReactRouterDOM;
    const styled = window.styled.default;

    // ================== Core Components ==================
    const TopNav = () => (
      <div style={{
        height: '60px',
        display: 'flex',
        alignItems: 'center',
        padding: '0 30px',
        background: var(--secondary-gray),
        justifyContent: 'space-between'
      }}>
        <input 
          type="text" 
          placeholder="Search..." 
          style={{
            background: var(--primary-bg),
            border: 'none',
            padding: '10px',
            borderRadius: '4px',
            color: 'white'
          }}
        />
        <div style={{ display: 'flex', alignItems: 'center', gap: '20px' }}>
          <button style={{ background: 'none', border: 'none', color: 'white' }}>
            🔔
          </button>
          <div style={{
            width: '40px',
            height: '40px',
            borderRadius: '50%',
            background: var(--accent-blue)
          }}></div>
        </div>
      </div>
    );

    // ================== Full Page Components ==================
    function TradingPage() {
      React.useEffect(() => {
        const chart = new ApexCharts(document.querySelector("#chart"), {
          chart: { type: 'candlestick', height: 400 },
          series: [{
            data: [
              { x: new Date(2024, 0, 1), y: [5000, 5100, 4900, 5050] },
              { x: new Date(2024, 0, 2), y: [5050, 5250, 5030, 5150] },
              { x: new Date(2024, 0, 3), y: [5150, 5350, 5100, 5250] }
            ]
          }],
          xaxis: { type: 'datetime' }
        });
        chart.render();
      }, []);

      return (
        <div style={{ display: 'flex', padding: '20px', gap: '20px' }}>
          <div style={{ flex: 2 }}>
            <div id="chart"></div>
          </div>
          
          <div style={{ flex: 1, background: var(--secondary-gray), padding: '20px', borderRadius: '8px' }}>
            <h2>Order Book</h2>
            <div style={{ marginTop: '20px' }}>
              <div style={{ display: 'flex', justifyContent: 'space-between', margin: '10px 0' }}>
                <span>Buy Orders</span>
                <span>Price</span>
              </div>
              {[5250, 5245, 5240].map((price) => (
                <div key={price} style={{
                  background: '#1c3238',
                  padding: '10px',
                  margin: '5px 0',
                  borderRadius: '4px'
                }}>
                  {price.toFixed(2)}
                </div>
              ))}
            </div>
          </div>
        </div>
      );
    }

    function TransactionsPage() {
      const transactions = [
        { date: '2024-02-20', amount: '$1,500.00', type: 'Deposit', status: 'Completed' },
        { date: '2024-02-19', amount: '$2,300.00', type: 'Withdrawal', status: 'Pending' }
      ];

      return (
        <div style={{ padding: '30px' }}>
          <div style={{ display: 'flex', justifyContent: 'space-between', marginBottom: '20px' }}>
            <div style={{ display: 'flex', gap: '10px' }}>
              <button style={{
                background: var(--accent-blue),
                border: 'none',
                padding: '10px 20px',
                borderRadius: '4px',
                color: 'white'
              }}>All</button>
              {['Deposit', 'Withdrawal', 'Transfer'].map(type => (
                <button key={type} style={{
                  background: var(--secondary-gray),
                  border: 'none',
                  padding: '10px 20px',
                  borderRadius: '4px',
                  color: 'white'
                }}>{type}</button>
              ))}
            </div>
            <button style={{
              background: var(--accent-blue),
              border: 'none',
              padding: '10px 20px',
              borderRadius: '4px',
              color: 'white'
            }}>Export CSV</button>
          </div>

          <table style={{ width: '100%', borderCollapse: 'collapse' }}>
            <thead>
              <tr style={{ borderBottom: '2px solid var(--accent-blue)' }}>
                <th style={{ textAlign: 'left', padding: '15px 0' }}>Date</th>
                <th style={{ textAlign: 'left' }}>Amount</th>
                <th style={{ textAlign: 'left' }}>Type</th>
                <th style={{ textAlign: 'left' }}>Status</th>
              </tr>
            </thead>
            <tbody>
              {transactions.map((tx, i) => (
                <tr key={i} className="table-row" style={{ padding: '15px 0' }}>
                  <td style={{ padding: '15px 0' }}>{tx.date}</td>
                  <td>{tx.amount}</td>
                  <td>{tx.type}</td>
                  <td style={{ color: tx.status === 'Completed' ? '#00C853' : '#FFD600' }}>
                    {tx.status}
                  </td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      );
    }

    function SettingsPage() {
      return (
        <div style={{ padding: '30px' }}>
          <div style={{
            background: var(--secondary-gray),
            padding: '20px',
            borderRadius: '8px',
            marginBottom: '30px'
          }}>
            <h2>Security Settings</h2>
            <div style={{ marginTop: '20px' }}>
              <input type="password" placeholder="New Password" style={{
                background: var(--primary-bg),
                border: 'none',
                padding: '10px',
                margin: '10px 0',
                width: '300px',
                color: 'white'
              }} />
              <div style={{ marginTop: '15px' }}>
                <button style={{
                  background: var(--accent-blue),
                  border: 'none',
                  padding: '10px 20px',
                  borderRadius: '4px',
                  color: 'white'
                }}>Change Password</button>
              </div>
            </div>
          </div>

          <div style={{
            background: var(--secondary-gray),
            padding: '20px',
            borderRadius: '8px'
          }}>
            <h2>Linked Accounts</h2>
            <div style={{ marginTop: '20px' }}>
              {['Bank of America', 'Coinbase Wallet'].map(account => (
                <div key={account} style={{
                  display: 'flex',
                  justifyContent: 'space-between',
                  alignItems: 'center',
                  padding: '15px 0',
                  borderBottom: '1px solid var(--primary-bg)'
                }}>
                  <span>{account}</span>
                  <button style={{
                    background: '#ff4444',
                    border: 'none',
                    padding: '8px 15px',
                    borderRadius: '4px',
                    color: 'white'
                  }}>Remove</button>
                </div>
              ))}
            </div>
          </div>
        </div>
      );
    }

    // Update main App component
    function App() {
      return (
        <BrowserRouter>
          <Routes>
            <Route path="/" element={<LoginPage />} />
            <Route path="/dashboard" element={<DashboardLayout />} />
          </Routes>
        </BrowserRouter>
      );
    }

    function DashboardLayout() {
      return (
        <div>
          <TopNav />
          <div style={{ display: 'flex' }}>
            <Sidebar />
            <div style={{ flex: 1 }}>
              <Routes>
                <Route path="/dashboard" element={<DashboardPage />} />
                <Route path="/transactions" element={<TransactionsPage />} />
                <Route path="/trading" element={<TradingPage />} />
                <Route path="/settings" element={<SettingsPage />} />
              </Routes>
            </div>
          </div>
        </div>
      );
    }

    // Previous components (LoginPage, Sidebar, etc.) remain unchanged
    // ... [Include all previous components from earlier answer here] ...

    ReactDOM.render(<App />, document.getElementById('root'));
  </script>
</body>
</html>