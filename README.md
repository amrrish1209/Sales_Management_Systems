# Sales_Management_Systems

Sales Management System developed using **Python**, **Streamlit**, and **PostgreSQL**. This system manages multi-branch sales operations, payment tracking, and real-time business analytics.

##  Implementation Details
1. Database Architecture (PostgreSQL)
I designed a relational database schema optimized for data integrity and performance. Key implementations include:
* **Custom Data Types:** Utilized PostgreSQL `ENUM` types for `sale_status` (Open/Close), `user_role` (Super Admin/Admin), and `payment_method_type` (Cash, UPI, Card) to ensure data consistency.
* **Relational Schema:** Created four interconnected tables: `branches`, `users`, `customer_sales`, and `payment_splits`.
* **Automated Calculations:** Implemented `GENERATED ALWAYS AS (gross_sales - received_amount) STORED` columns to automatically handle real-time balance calculations.

###  Database Automation & Logic
To ensure the application remains "data-accurate" without manual intervention:
* **PL/pgSQL Functions:** Wrote a custom function `update_received_amount()` that aggregates all payments for a specific sale.
* **Database Triggers:** Created an `AFTER INSERT` trigger (`trg_update_received_amount`) on the payments table. Every time a new payment is recorded, the customer's total received amount and pending balance update automatically at the database level.

### Application Features (Streamlit)
I built a multi-functional web dashboard featuring:
* **Secure Authentication:** A login portal with role-based access control. Users are directed to specific views based on their assigned branch and role.
* **Operational Management:**
    * **Add Sales:** Interface for entering new customer transactions.
    * **Payment Portal:** A dedicated section to log payment installments which triggers automatic background updates.
    * **View Sales:** A searchable data table for monitoring branch-specific or global sales.
* **Advanced Analytics & Reporting:**
    * **KPI Metrics:** Top-level dashboard showing Total Sales, Total Received, and Total Pending amounts.
    * **Visual Insights:** Built-in charts for Revenue per Branch, Payment Method Analysis, and Monthly Sales Trends.
    * **SQL Explorer:** A built-in query runner to execute pre-defined complex SQL analysis directly from the UI.
