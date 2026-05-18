# 💊 Pharmacy Management System

A desktop-based Pharmacy Management System built with **C# .NET Framework (Windows Forms)** and **SQL Server (LocalDB)**. The system supports three user roles — Customer, Pharmacist, and Admin — each with their own dedicated dashboard and features.

---

## 🖥️ Technology Stack

- **Language:** C# (.NET Framework 4.7.2)
- **UI Framework:** Windows Forms (WinForms)
- **Database:** SQL Server LocalDB (MSSQLLocalDB)
- **IDE:** Visual Studio
- **Database Access:** ADO.NET (SqlConnection, SqlCommand, SqlDataAdapter)

---

## 👥 User Roles

| Role | Description |
|---|---|
| **Customer** | Browse medicines, manage cart, place orders, upload prescriptions, view invoices |
| **Pharmacist** | Manage inventory, process orders, review prescriptions |
| **Admin** | Full control — manage medicines, orders, users, prescriptions, view reports |

---

## ✨ Features

### 🔐 Authentication
- Login with username and password
- Role-based routing — Customer, Admin, Pharmacist each go to their own dashboard
- Register new account
- Forgot password / reset password

### 👤 Customer Dashboard
- **Home** — welcome screen with quick stats and browse button
- **Medicines** — browse all medicines with images, search by name or category, add to cart
- **My Cart** — view cart items, update quantity, remove items, place order
- **My Orders** — view all past orders with status (Pending / Processing / Delivered)
- **Invoices** — view detailed invoice for each order with itemized breakdown
- **Prescriptions** — upload prescription images, view upload history and status
- **My Profile** — update personal info, change password

### 💊 Pharmacist Dashboard
- **Home** — stat cards (total medicines, low stock, pending orders, pending prescriptions)
- **Inventory** — view all medicines, restock items, delete medicines, search
- **Orders** — view and update order status (Pending → Processing → Delivered)
- **Prescriptions** — approve or reject customer prescriptions
- **My Profile** — update personal info, change password

### 🛠️ Admin Dashboard
- **Home** — overview cards (total users, medicines, orders, revenue)
- **Medicines** — add, edit, delete medicines, upload medicine images
- **Orders** — view all orders with itemized details, update order status
- **Prescriptions** — approve, reject, or delete prescriptions
- **Users** — view all registered users, delete users
- **Reports** — revenue stats, delivered/pending order counts, top selling medicines table
- **My Profile** — update personal info, change password

---

## 🗄️ Database Structure

The database is named **PharmacyDB** and contains the following tables:

| Table | Purpose |
|---|---|
| `Users` | Stores all user accounts with role (Customer / Admin / Pharmacist) |
| `Medicines` | Medicine catalog with name, category, price, stock, image |
| `Cart` | Temporary cart items per user |
| `OrderHeaders` | One record per order (total price, status, date) |
| `OrderItems` | Individual medicine items inside each order |
| `Orders` | Legacy order table |
| `Prescriptions` | Uploaded prescription files per user |

---

## ⚙️ Project Structure

```
PharmacyUser/
│
├── PharmacyUser.sln              Solution file
│
└── PharmacyUser/
    ├── Program.cs                Entry point — launches LoginForm
    ├── App.config                Database connection string
    ├── DBHelper.cs               All database operations (static helper class)
    │
    ├── LoginForm.cs              Login screen with role-based routing
    ├── RegisterForm.cs           New user registration
    ├── ForgotPasswordForm.cs     Password reset
    │
    ├── CustomerDashboard.cs      Full customer panel
    ├── PharmacistDashboard.cs    Full pharmacist panel
    ├── AdminDashboard.cs         Full admin panel
    │
    └── Properties/
        └── AssemblyInfo.cs
```

---

## 🚀 Getting Started

### Prerequisites

- Visual Studio 2019 or later
- .NET Framework 4.7.2
- SQL Server LocalDB (comes with Visual Studio)

### Setup Steps

**1. Clone the repository**
```
git clone https:[//github.com/your-username/PharmacyUser.git](https://github.com/rudbaanika2580/PharmacyUser)
```

**2. Set up the database**

Open SQL Server Management Studio (SSMS) or use the LocalDB query tool and run the provided SQL script:
```
PharmacyDB_Script.sql
```
This will create the `PharmacyDB` database with all tables and sample data automatically.

**3. Check the connection string**

Open `App.config` and verify the connection string matches your LocalDB instance:
```xml
<connectionStrings>
    <add name="Pharmacy"
         connectionString="Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=Pharmacy;Integrated Security=True"
         providerName="System.Data.SqlClient" />
</connectionStrings>
```

**4. Open and run the project**

Open `PharmacyUser.sln` in Visual Studio and press **F5** to build and run.

---

## 🔑 Default Login Credentials

| Username | Password | Role |
|---|---|---|
| `rizwanul` | `1` | Customer |
| `rudba` | `1` | Admin |
| `faisal` | `1` | Pharmacist |


---

## 📁 Medicine Images

Medicine images are stored locally in:
```
bin/Debug/MedicineImages/
```
The Admin panel allows uploading new images for each medicine directly from the UI. Images are saved to this folder and the path is stored in the database.

---

## 🏗️ OOP Concepts Used

- **Inheritance** — All dashboard forms inherit from `Form` (e.g. `AdminDashboard : Form`)
- **Encapsulation** — Private fields for colors and panels; public properties for user data
- **Abstraction** — `DBHelper` hides all database logic; each `Show___()` method hides section complexity
- **Polymorphism** — Same `Click`/`Paint` events with different behavior per button/panel; `DrawCard()` method works on any panel

---

## 🗃️ Full Database SQL Script

```

> **Note:** The `ImagePath` values in the Medicines and Prescriptions insert statements have been left blank intentionally. After running the script, use the Admin panel to upload medicine images from your local machine.

---

## 📄 License

This project is for educational purposes.

---

> Built with ❤️ using C# Windows Forms — Pharmacy © 2026
