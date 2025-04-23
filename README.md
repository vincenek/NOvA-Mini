<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NOvA-X Financial Interface</title>
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <style>
        :root {
            --primary-color: #2A2A72;
            --secondary-color: #009FFD;
            --accent-color: #00C49A;
        }

        body {
            margin: 0;
            font-family: 'Segoe UI', sans-serif;
            display: grid;
            grid-template-columns: 240px 1fr;
            min-height: 100vh;
        }

        /* Navigation Sidebar */
        .nav-sidebar {
            background: var(--primary-color);
            color: white;
            padding: 2rem;
            position: fixed;
            height: 100%;
            width: 240px;
        }

        .nav-header {
            font-size: 1.8rem;
            font-weight: bold;
            margin-bottom: 2rem;
        }

        .nav-item {
            display: flex;
            align-items: center;
            gap: 1rem;
            padding: 1rem;
            margin: 0.5rem 0;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .nav-item:hover {
            background: var(--secondary-color);
        }

        .ask-anything {
            position: absolute;
            bottom: 2rem;
            width: calc(100% - 4rem);
        }

        /* Main Content Area */
        .main-content {
            padding: 2rem;
            background: #f5f7fb;
        }

        /* Section Styling */
        .content-section {
            display: none;
            background: white;
            border-radius: 12px;
            padding: 2rem;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        .active-section {
            display: block;
        }
    </style>
</head>
<body>
    <!-- Navigation Sidebar -->
    <nav class="nav-sidebar">
        <div class="nav-header">NOvA-X</div>
        
        <div class="nav-item" onclick="showSection('wallet')">
            <span class="material-icons">account_balance_wallet</span>
            Wallet
        </div>
        
        <div class="nav-item" onclick="showSection('transfer')">
            <span class="material-icons">swap_horiz</span>
            Transfer
        </div>
        
        <div class="nav-item" onclick="showSection('budgeting')">
            <span class="material-icons">pie_chart</span>
            Budgeting/Goals
        </div>
        
        <div class="nav-item" onclick="showSection('settings')">
            <span class="material-icons">settings</span>
            Setting
        </div>

        <div class="ask-anything">
            <input type="text" placeholder="Ask anything..." style="width: 100%; padding: 12px; border-radius: 25px; border: none;">
        </div>
    </nav>

    <!-- Main Content Sections -->
    <main class="main-content">
        <!-- Wallet Section -->
        <section id="wallet" class="content-section active-section">
            <!-- Wallet content from previous implementation -->
        </section>

        <!-- Transfer Section -->
        <section id="transfer" class="content-section">
            <!-- Transfer content from previous implementation -->
        </section>

        <!-- Budgeting Section -->
        <section id="budgeting" class="content-section">
            <!-- Budgeting content from previous implementation -->
        </section>

        <!-- Settings Section -->
        <section id="settings" class="content-section">
            <!-- Settings content from previous implementation -->
        </section>
    </main>

    <script>
        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.content-section').forEach(section => {
                section.classList.remove('active-section');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active-section');
        }
    </script>
</body>
</html>
