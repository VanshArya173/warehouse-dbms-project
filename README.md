# 🏭 Kirana Mart — Warehouse DBMS Project

A full-stack warehouse-centric supply chain management system built as a DBMS coursework project at IIITD. Features a multi-role architecture, ACID-compliant transactions, real-time analytics, and a complete audit trail.

---

## 🧑‍🤝‍🧑 Roles & What They Can Do

| Role | Capabilities |
|------|-------------|
| **Producer** | Register products, set prices, fulfil restock requests, request price changes, track shipments & earnings |
| **Warehouse Staff** | Send restock requests to producers, approve/reject price changes, manage inventory, track orders, top up budget |
| **Customer** | Browse catalogue, place orders, track order status, manage wallet balance |
| **Manager** | Approve/reject producers, oversee all operations across dashboards |

---

## ✨ Features

- 🔐 **Auth system** — bcrypt-hashed passwords, role-based login, separate auth DB
- 📦 **Inventory management** — real-time stock tracking with reserved & available quantities
- 🔄 **Restock workflow** — warehouse sends requests → producer quotes price → warehouse approves → batch created
- 💰 **Price change requests** — producers request price changes, warehouse approves/rejects
- 🧾 **ACID transactions** — order placement, delivery, and budget updates are fully transactional with rollback on failure
- 📊 **Analytics dashboard** — window functions (RANK, DENSE_RANK, ROW_NUMBER), running totals, GROUP BY ROLLUP, recursive CTEs for category trees
- 🛡️ **Audit log** — every critical DB change is tracked in `Audit_Log` table
- 🧮 **Custom SQL functions** — `fn_price_with_tax()`, `fn_stock_available()`, `fn_producer_total_revenue()`
- 📉 **Low stock alerts** — via `v_low_stock_products` view
- 💳 **Wallet system** — customers have a wallet; balance deducted on order, refunded on cancellation

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Python, Flask |
| Database | MySQL (two DBs: `supplychain_db` + `auth_db`) |
| Frontend | HTML, CSS, JavaScript (Jinja2 templates) |
| Auth | bcrypt password hashing |

---

## 📁 Project Structure

```
warehouse-dbms-project/
├── app.py              # Flask backend — all routes (1700+ lines)
├── db/                 # SQL schema, triggers, views, functions, seed data
├── templates/
│   ├── admin/          # Warehouse dashboard, analytics, producer management
│   ├── producer/       # Producer dashboard
│   ├── customer/       # Customer dashboard & store
│   └── auth/           # Login & signup pages
├── static/             # CSS and JS assets
├── docs/               # Project documentation
└── requirements.txt    # Python dependencies
```

---

## 🚀 Run Locally

```bash
# 1. Clone the repo
git clone https://github.com/VanshArya173/warehouse-dbms-project.git
cd warehouse-dbms-project

# 2. Install dependencies
pip install -r requirements.txt

# 3. Set up MySQL
# Create supplychain_db and auth_db
# Run the SQL files in /db in order (schema → data → triggers → views → functions)

# 4. Update DB credentials in app.py
# host="localhost", user="root", password="your_password"

# 5. Start the server
python app.py
```

Then open `http://localhost:5000` in your browser.

---

## 🗄️ Database Highlights

- **Normalised schema** — Producer, Product, Warehouse, Inventory, Batch, Order, Order_Item, Wallet, Restock_Request, Price_Change_Request, Audit_Log
- **Triggers** — auto-update inventory on batch arrival, auto-log changes to Audit_Log
- **Views** — `v_low_stock_products`, `v_warehouse_summary`
- **Stored functions** — price with GST, stock availability, producer revenue
- **Window functions** — RANK, DENSE_RANK, ROW_NUMBER, running totals over batches
- **Recursive CTE** — category tree traversal
- **ROLLUP** — multi-level revenue aggregation by producer and product
- **Two databases** — `supplychain_db` for business data, `auth_db` for user credentials (separation of concerns)

---


