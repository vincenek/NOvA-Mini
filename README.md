import sqlite3
import getpass
import datetime

DB_NAME = 'wallet.db'

def init_db():
    with sqlite3.connect(DB_NAME) as conn:
        c = conn.cursor()
        c.execute('''
        CREATE TABLE IF NOT EXISTS users (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            username TEXT UNIQUE,
            password TEXT,
            balance REAL DEFAULT 0.0
        )
        ''')
        c.execute('''
        CREATE TABLE IF NOT EXISTS transactions (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            user_id INTEGER,
            type TEXT,
            amount REAL,
            to_user TEXT,
            timestamp TEXT,
            FOREIGN KEY(user_id) REFERENCES users(id)
        )
        ''')
    print("[✔] Database initialized.")

def register():
    username = input("Choose username: ")
    password = getpass.getpass("Choose password: ")
    with sqlite3.connect(DB_NAME) as conn:
        c = conn.cursor()
        try:
            c.execute("INSERT INTO users (username, password) VALUES (?, ?)", (username, password))
            conn.commit()
            print("[+] Registration successful.")
        except sqlite3.IntegrityError:
            print("[!] Username already taken.")

def login():
    username = input("Username: ")
    password = getpass.getpass("Password: ")
    with sqlite3.connect(DB_NAME) as conn:
        c = conn.cursor()
        c.execute("SELECT id FROM users WHERE username = ? AND password = ?", (username, password))
        user = c.fetchone()
        if user:
            print("[✔] Login successful.")
            return user[0], username
        else:
            print("[!] Invalid credentials.")
            return None, None

def get_balance(user_id):
    with sqlite3.connect(DB_NAME) as conn:
        c = conn.cursor()
        c.execute("SELECT balance FROM users WHERE id = ?", (user_id,))
        return c.fetchone()[0]

def update_balance(user_id, amount):
    with sqlite3.connect(DB_NAME) as conn:
        c = conn.cursor()
        c.execute("UPDATE users SET balance = balance + ? WHERE id = ?", (amount, user_id))
        conn.commit()

def record_transaction(user_id, tx_type, amount, to_user=''):
    with sqlite3.connect(DB_NAME) as conn:
        c = conn.cursor()
        c.execute("INSERT INTO transactions (user_id, type, amount, to_user, timestamp) VALUES (?, ?, ?, ?, ?)",
                  (user_id, tx_type, amount, to_user, datetime.datetime.now().isoformat()))
        conn.commit()

def deposit(user_id):
    amount = float(input("Amount to deposit: "))
    update_balance(user_id, amount)
    record_transaction(user_id, 'DEPOSIT', amount)
    print(f"[+] Deposited ${amount:.2f}")

def withdraw(user_id):
    amount = float(input("Amount to withdraw: "))
    if get_balance(user_id) >= amount:
        update_balance(user_id, -amount)
        record_transaction(user_id, 'WITHDRAW', amount)
        print(f"[-] Withdrew ${amount:.2f}")
    else:
        print("[!] Insufficient funds.")

def transfer(user_id, username):
    to_user = input("Transfer to (username): ")
    amount = float(input("Amount to transfer: "))
    with sqlite3.connect(DB_NAME) as conn:
        c = conn.cursor()
        c.execute("SELECT id FROM users WHERE username = ?", (to_user,))
        recipient = c.fetchone()
        if not recipient:
            print("[!] Recipient not found.")
            return
        if get_balance(user_id) < amount:
            print("[!] Insufficient funds.")
            return
        update_balance(user_id, -amount)
        update_balance(recipient[0], amount)
        record_transaction(user_id, 'TRANSFER_OUT', amount, to_user)
        record_transaction(recipient[0], 'TRANSFER_IN', amount, username)
        print(f"[→] Transferred ${amount:.2f} to {to_user}")

def transaction_history(user_id):
    with sqlite3.connect(DB_NAME) as conn:
        c = conn.cursor()
        c.execute("SELECT type, amount, to_user, timestamp FROM transactions WHERE user_id = ? ORDER BY timestamp DESC", (user_id,))
        txs = c.fetchall()
        if not txs:
            print("[!] No transactions found.")
            return
        print("\n--- Transaction History ---")
        for tx in txs:
            print(f"{tx[3]} | {tx[0]} | ${tx[1]:.2f} | To: {tx[2] if tx[2] else 'N/A'}")

def wallet_menu(user_id, username):
    while True:
        print(f"\n--- Welcome {username} ---")
        print("1. Check Balance")
        print("2. Deposit")
        print("3. Withdraw")
        print("4. Transfer")
        print("5. View Transactions")
        print("6. Logout")
        choice = input("Choose: ")
        if choice == '1':
            print(f"[$] Balance: ${get_balance(user_id):.2f}")
        elif choice == '2':
            deposit(user_id)
        elif choice == '3':
            withdraw(user_id)
        elif choice == '4':
            transfer(user_id, username)
        elif choice == '5':
            transaction_history(user_id)
        elif choice == '6':
            break
        else:
            print("[!] Invalid option.")

def main():
    init_db()
    while True:
        print("\n=== Bank Wallet App ===")
        print("1. Register")
        print("2. Login")
        print("3. Exit")
        choice = input("Choose: ")
        if choice == '1':
            register()
        elif choice == '2':
            user_id, username = login()
            if user_id:
                wallet_menu(user_id, username)
        elif choice == '3':
            print("Goodbye!")
            break
        else:
            print("[!] Invalid option.")

if __name__ == '__main__':
    main()
Initial commit - Python CLI wallet app