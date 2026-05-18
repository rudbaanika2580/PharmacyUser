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
    <add name="PharmacyDB"
         connectionString="Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=PharmacyDB;Integrated Security=True"
         providerName="System.Data.SqlClient" />
</connectionStrings>
```

**4. Open and run the project**

Open `PharmacyUser.sln` in Visual Studio and press **F5** to build and run.

---

## 🔑 Default Login Credentials

| Username | Password | Role |
|---|---|---|
| `akib` | `1` | Customer |
| `arnob` | `1` | Admin |
| `tonmoy` | `1` | Pharmacist |
| `kulas` | `1` | Admin |

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

Run the following script in SQL Server Management Studio (SSMS) to create and populate the entire database from scratch.

```sql
USE [master]
GO
IF EXISTS (SELECT name FROM sys.databases WHERE name = N'PharmacyDB')
BEGIN
    ALTER DATABASE [PharmacyDB] SET SINGLE_USER WITH ROLLBACK IMMEDIATE
    DROP DATABASE [PharmacyDB]
END
GO

CREATE DATABASE [PharmacyDB]
GO
ALTER DATABASE [PharmacyDB] SET COMPATIBILITY_LEVEL = 150
GO
IF (1 = FULLTEXTSERVICEPROPERTY('IsFullTextInstalled'))
begin
EXEC [PharmacyDB].[dbo].[sp_fulltext_database] @action = 'enable'
end
GO
ALTER DATABASE [PharmacyDB] SET ANSI_NULL_DEFAULT OFF 
GO
ALTER DATABASE [PharmacyDB] SET ANSI_NULLS OFF 
GO
ALTER DATABASE [PharmacyDB] SET ANSI_PADDING OFF 
GO
ALTER DATABASE [PharmacyDB] SET ANSI_WARNINGS OFF 
GO
ALTER DATABASE [PharmacyDB] SET ARITHABORT OFF 
GO
ALTER DATABASE [PharmacyDB] SET AUTO_CLOSE ON 
GO
ALTER DATABASE [PharmacyDB] SET AUTO_SHRINK OFF 
GO
ALTER DATABASE [PharmacyDB] SET AUTO_UPDATE_STATISTICS ON 
GO
ALTER DATABASE [PharmacyDB] SET CURSOR_CLOSE_ON_COMMIT OFF 
GO
ALTER DATABASE [PharmacyDB] SET CURSOR_DEFAULT  GLOBAL 
GO
ALTER DATABASE [PharmacyDB] SET CONCAT_NULL_YIELDS_NULL OFF 
GO
ALTER DATABASE [PharmacyDB] SET NUMERIC_ROUNDABORT OFF 
GO
ALTER DATABASE [PharmacyDB] SET QUOTED_IDENTIFIER OFF 
GO
ALTER DATABASE [PharmacyDB] SET RECURSIVE_TRIGGERS OFF 
GO
ALTER DATABASE [PharmacyDB] SET  ENABLE_BROKER 
GO
ALTER DATABASE [PharmacyDB] SET AUTO_UPDATE_STATISTICS_ASYNC OFF 
GO
ALTER DATABASE [PharmacyDB] SET DATE_CORRELATION_OPTIMIZATION OFF 
GO
ALTER DATABASE [PharmacyDB] SET TRUSTWORTHY OFF 
GO
ALTER DATABASE [PharmacyDB] SET ALLOW_SNAPSHOT_ISOLATION OFF 
GO
ALTER DATABASE [PharmacyDB] SET PARAMETERIZATION SIMPLE 
GO
ALTER DATABASE [PharmacyDB] SET READ_COMMITTED_SNAPSHOT OFF 
GO
ALTER DATABASE [PharmacyDB] SET HONOR_BROKER_PRIORITY OFF 
GO
ALTER DATABASE [PharmacyDB] SET RECOVERY SIMPLE 
GO
ALTER DATABASE [PharmacyDB] SET  MULTI_USER 
GO
ALTER DATABASE [PharmacyDB] SET PAGE_VERIFY CHECKSUM  
GO
ALTER DATABASE [PharmacyDB] SET DB_CHAINING OFF 
GO
ALTER DATABASE [PharmacyDB] SET FILESTREAM( NON_TRANSACTED_ACCESS = OFF ) 
GO
ALTER DATABASE [PharmacyDB] SET TARGET_RECOVERY_TIME = 60 SECONDS 
GO
ALTER DATABASE [PharmacyDB] SET DELAYED_DURABILITY = DISABLED 
GO
ALTER DATABASE [PharmacyDB] SET ACCELERATED_DATABASE_RECOVERY = OFF  
GO
ALTER DATABASE [PharmacyDB] SET QUERY_STORE = OFF
GO
USE [PharmacyDB]
GO
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Cart](
	[CartID] [int] IDENTITY(1,1) NOT NULL,
	[UserID] [int] NOT NULL,
	[MedicineID] [int] NOT NULL,
	[Quantity] [int] NOT NULL,
PRIMARY KEY CLUSTERED 
(
	[CartID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Medicines](
	[MedicineID] [int] IDENTITY(1,1) NOT NULL,
	[Name] [nvarchar](100) NOT NULL,
	[Category] [nvarchar](50) NOT NULL,
	[Price] [decimal](10, 2) NOT NULL,
	[Stock] [int] NOT NULL,
	[Description] [nvarchar](200) NULL,
	[ImagePath] [nvarchar](500) NULL,
	[MedicineImage] [varbinary](max) NULL,
PRIMARY KEY CLUSTERED 
(
	[MedicineID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[OrderHeaders](
	[OrderHeaderID] [int] IDENTITY(1,1) NOT NULL,
	[UserID] [int] NOT NULL,
	[TotalPrice] [decimal](10, 2) NOT NULL,
	[Status] [nvarchar](20) NOT NULL,
	[OrderDate] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[OrderHeaderID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[OrderItems](
	[OrderItemID] [int] IDENTITY(1,1) NOT NULL,
	[OrderHeaderID] [int] NOT NULL,
	[MedicineName] [nvarchar](100) NOT NULL,
	[Quantity] [int] NOT NULL,
	[UnitPrice] [decimal](10, 2) NOT NULL,
	[TotalPrice] [decimal](10, 2) NOT NULL,
PRIMARY KEY CLUSTERED 
(
	[OrderItemID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Orders](
	[OrderID] [int] IDENTITY(1,1) NOT NULL,
	[UserID] [int] NULL,
	[MedicineName] [nvarchar](100) NOT NULL,
	[Quantity] [int] NOT NULL,
	[TotalPrice] [decimal](10, 2) NOT NULL,
	[Status] [nvarchar](20) NOT NULL,
	[OrderDate] [datetime] NULL,
PRIMARY KEY CLUSTERED 
(
	[OrderID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Prescriptions](
	[PrescriptionID] [int] IDENTITY(1,1) NOT NULL,
	[UserID] [int] NOT NULL,
	[FileName] [nvarchar](200) NOT NULL,
	[FilePath] [nvarchar](500) NOT NULL,
	[UploadDate] [datetime] NULL,
	[Status] [nvarchar](20) NULL,
PRIMARY KEY CLUSTERED 
(
	[PrescriptionID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Users](
	[UserID] [int] IDENTITY(1,1) NOT NULL,
	[FirstName] [nvarchar](50) NOT NULL,
	[LastName] [nvarchar](50) NOT NULL,
	[Username] [nvarchar](50) NOT NULL,
	[Email] [nvarchar](100) NOT NULL,
	[Phone] [nvarchar](20) NOT NULL,
	[Password] [nvarchar](100) NOT NULL,
	[Role] [nvarchar](20) NOT NULL,
PRIMARY KEY CLUSTERED 
(
	[UserID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
SET IDENTITY_INSERT [dbo].[Medicines] ON 

INSERT [dbo].[Medicines] ([MedicineID], [Name], [Category], [Price], [Stock], [Description], [ImagePath], [MedicineImage]) VALUES (1, N'Paracetamol 500mg', N'Pain Relief', CAST(60.00 AS Decimal(10, 2)), 15, N'Used for fever and mild pain', N'', NULL)
INSERT [dbo].[Medicines] ([MedicineID], [Name], [Category], [Price], [Stock], [Description], [ImagePath], [MedicineImage]) VALUES (2, N'Vitamin C 1000mg', N'Vitamins', CAST(85.00 AS Decimal(10, 2)), 140, N'Boosts immune system', N'', NULL)
INSERT [dbo].[Medicines] ([MedicineID], [Name], [Category], [Price], [Stock], [Description], [ImagePath], [MedicineImage]) VALUES (3, N'Amoxicillin 250mg', N'Antibiotic', CAST(150.00 AS Decimal(10, 2)), 50, N'Treats bacterial infections', N'', NULL)
INSERT [dbo].[Medicines] ([MedicineID], [Name], [Category], [Price], [Stock], [Description], [ImagePath], [MedicineImage]) VALUES (4, N'Vitamin D3', N'Vitamins', CAST(150.00 AS Decimal(10, 2)), 70, N'Supports bone health', N'', NULL)
INSERT [dbo].[Medicines] ([MedicineID], [Name], [Category], [Price], [Stock], [Description], [ImagePath], [MedicineImage]) VALUES (5, N'Atova 10mg', N'Atorvastatin Calcium', CAST(162.00 AS Decimal(10, 2)), 50, N'Supports immune function', N'', NULL)
INSERT [dbo].[Medicines] ([MedicineID], [Name], [Category], [Price], [Stock], [Description], [ImagePath], [MedicineImage]) VALUES (6, N'Omeprazole 20mg', N'Antacid', CAST(75.00 AS Decimal(10, 2)), 1040, N'Treats acid reflux', N'', NULL)
INSERT [dbo].[Medicines] ([MedicineID], [Name], [Category], [Price], [Stock], [Description], [ImagePath], [MedicineImage]) VALUES (7, N'Ibuprofen 400mg', N'Pain Relief', CAST(70.00 AS Decimal(10, 2)), 50, N'Anti-inflammatory pain relief', N'', NULL)
INSERT [dbo].[Medicines] ([MedicineID], [Name], [Category], [Price], [Stock], [Description], [ImagePath], [MedicineImage]) VALUES (8, N'Cetirizine 10mg', N'Antihistamine', CAST(55.00 AS Decimal(10, 2)), 110, N'Treats allergies', N'', NULL)
SET IDENTITY_INSERT [dbo].[Medicines] OFF
GO
SET IDENTITY_INSERT [dbo].[OrderHeaders] ON 

INSERT [dbo].[OrderHeaders] ([OrderHeaderID], [UserID], [TotalPrice], [Status], [OrderDate]) VALUES (1, 1, CAST(1305.00 AS Decimal(10, 2)), N'Delivered', CAST(N'2026-05-09T20:47:25.850' AS DateTime))
INSERT [dbo].[OrderHeaders] ([OrderHeaderID], [UserID], [TotalPrice], [Status], [OrderDate]) VALUES (2, 1, CAST(4522.00 AS Decimal(10, 2)), N'Delivered', CAST(N'2026-05-09T21:04:02.300' AS DateTime))
INSERT [dbo].[OrderHeaders] ([OrderHeaderID], [UserID], [TotalPrice], [Status], [OrderDate]) VALUES (3, 1, CAST(1305.00 AS Decimal(10, 2)), N'Pending', CAST(N'2026-05-09T21:46:17.863' AS DateTime))
INSERT [dbo].[OrderHeaders] ([OrderHeaderID], [UserID], [TotalPrice], [Status], [OrderDate]) VALUES (4, 1, CAST(1305.00 AS Decimal(10, 2)), N'Pending', CAST(N'2026-05-09T22:05:13.327' AS DateTime))
INSERT [dbo].[OrderHeaders] ([OrderHeaderID], [UserID], [TotalPrice], [Status], [OrderDate]) VALUES (5, 1, CAST(1035.00 AS Decimal(10, 2)), N'Pending', CAST(N'2026-05-10T12:37:21.643' AS DateTime))
INSERT [dbo].[OrderHeaders] ([OrderHeaderID], [UserID], [TotalPrice], [Status], [OrderDate]) VALUES (6, 1, CAST(2252.50 AS Decimal(10, 2)), N'Pending', CAST(N'2026-05-10T12:50:41.290' AS DateTime))
SET IDENTITY_INSERT [dbo].[OrderHeaders] OFF
GO
SET IDENTITY_INSERT [dbo].[OrderItems] ON 

INSERT [dbo].[OrderItems] ([OrderItemID], [OrderHeaderID], [MedicineName], [Quantity], [UnitPrice], [TotalPrice]) VALUES (1, 1, N'Paracetamol 500mg', 10, CAST(60.00 AS Decimal(10, 2)), CAST(600.00 AS Decimal(10, 2)))
INSERT [dbo].[OrderItems] ([OrderItemID], [OrderHeaderID], [MedicineName], [Quantity], [UnitPrice], [TotalPrice]) VALUES (2, 1, N'Vitamin C 1000mg', 10, CAST(85.00 AS Decimal(10, 2)), CAST(850.00 AS Decimal(10, 2)))
INSERT [dbo].[OrderItems] ([OrderItemID], [OrderHeaderID], [MedicineName], [Quantity], [UnitPrice], [TotalPrice]) VALUES (3, 2, N'Paracetamol 500mg', 10, CAST(60.00 AS Decimal(10, 2)), CAST(600.00 AS Decimal(10, 2)))
INSERT [dbo].[OrderItems] ([OrderItemID], [OrderHeaderID], [MedicineName], [Quantity], [UnitPrice], [TotalPrice]) VALUES (4, 2, N'Vitamin C 1000mg', 10, CAST(85.00 AS Decimal(10, 2)), CAST(850.00 AS Decimal(10, 2)))
INSERT [dbo].[OrderItems] ([OrderItemID], [OrderHeaderID], [MedicineName], [Quantity], [UnitPrice], [TotalPrice]) VALUES (5, 2, N'Vitamin D3', 10, CAST(150.00 AS Decimal(10, 2)), CAST(1500.00 AS Decimal(10, 2)))
INSERT [dbo].[OrderItems] ([OrderItemID], [OrderHeaderID], [MedicineName], [Quantity], [UnitPrice], [TotalPrice]) VALUES (6, 2, N'Atova 10mg', 10, CAST(162.00 AS Decimal(10, 2)), CAST(1620.00 AS Decimal(10, 2)))
INSERT [dbo].[OrderItems] ([OrderItemID], [OrderHeaderID], [MedicineName], [Quantity], [UnitPrice], [TotalPrice]) VALUES (7, 2, N'Omeprazole 20mg', 10, CAST(75.00 AS Decimal(10, 2)), CAST(750.00 AS Decimal(10, 2)))
INSERT [dbo].[OrderItems] ([OrderItemID], [OrderHeaderID], [MedicineName], [Quantity], [UnitPrice], [TotalPrice]) VALUES (8, 3, N'Paracetamol 500mg', 10, CAST(60.00 AS Decimal(10, 2)), CAST(600.00 AS Decimal(10, 2)))
INSERT [dbo].[OrderItems] ([OrderItemID], [OrderHeaderID], [MedicineName], [Quantity], [UnitPrice], [TotalPrice]) VALUES (9, 3, N'Vitamin C 1000mg', 10, CAST(85.00 AS Decimal(10, 2)), CAST(850.00 AS Decimal(10, 2)))
INSERT [dbo].[OrderItems] ([OrderItemID], [OrderHeaderID], [MedicineName], [Quantity], [UnitPrice], [TotalPrice]) VALUES (10, 4, N'Paracetamol 500mg', 10, CAST(60.00 AS Decimal(10, 2)), CAST(600.00 AS Decimal(10, 2)))
INSERT [dbo].[OrderItems] ([OrderItemID], [OrderHeaderID], [MedicineName], [Quantity], [UnitPrice], [TotalPrice]) VALUES (11, 4, N'Vitamin C 1000mg', 10, CAST(85.00 AS Decimal(10, 2)), CAST(850.00 AS Decimal(10, 2)))
INSERT [dbo].[OrderItems] ([OrderItemID], [OrderHeaderID], [MedicineName], [Quantity], [UnitPrice], [TotalPrice]) VALUES (12, 5, N'Paracetamol 500mg', 5, CAST(60.00 AS Decimal(10, 2)), CAST(300.00 AS Decimal(10, 2)))
INSERT [dbo].[OrderItems] ([OrderItemID], [OrderHeaderID], [MedicineName], [Quantity], [UnitPrice], [TotalPrice]) VALUES (13, 5, N'Vitamin C 1000mg', 10, CAST(85.00 AS Decimal(10, 2)), CAST(850.00 AS Decimal(10, 2)))
INSERT [dbo].[OrderItems] ([OrderItemID], [OrderHeaderID], [MedicineName], [Quantity], [UnitPrice], [TotalPrice]) VALUES (14, 6, N'Cetirizine 10mg', 10, CAST(55.00 AS Decimal(10, 2)), CAST(550.00 AS Decimal(10, 2)))
INSERT [dbo].[OrderItems] ([OrderItemID], [OrderHeaderID], [MedicineName], [Quantity], [UnitPrice], [TotalPrice]) VALUES (15, 6, N'Vitamin D3', 10, CAST(150.00 AS Decimal(10, 2)), CAST(1500.00 AS Decimal(10, 2)))
INSERT [dbo].[OrderItems] ([OrderItemID], [OrderHeaderID], [MedicineName], [Quantity], [UnitPrice], [TotalPrice]) VALUES (16, 6, N'Paracetamol 500mg', 10, CAST(60.00 AS Decimal(10, 2)), CAST(600.00 AS Decimal(10, 2)))
SET IDENTITY_INSERT [dbo].[OrderItems] OFF
GO
SET IDENTITY_INSERT [dbo].[Prescriptions] ON 

INSERT [dbo].[Prescriptions] ([PrescriptionID], [UserID], [FileName], [FilePath], [UploadDate], [Status]) VALUES (7, 1, N'WhatsApp Image 2026-04-05 at 10.03.56 PM.jpeg', N'', CAST(N'2026-05-09T21:46:55.370' AS DateTime), N'Pending')
SET IDENTITY_INSERT [dbo].[Prescriptions] OFF
GO
SET IDENTITY_INSERT [dbo].[Users] ON 

INSERT [dbo].[Users] ([UserID], [FirstName], [LastName], [Username], [Email], [Phone], [Password], [Role]) VALUES (1, N'akib', N'hossain', N'akib', N'akibh274@gmail.com', N'0123456789', N'1', N'Customer')
INSERT [dbo].[Users] ([UserID], [FirstName], [LastName], [Username], [Email], [Phone], [Password], [Role]) VALUES (3, N'arnob', N'das', N'arnob', N'arnob@gmail.com', N'01234567', N'1', N'Admin')
INSERT [dbo].[Users] ([UserID], [FirstName], [LastName], [Username], [Email], [Phone], [Password], [Role]) VALUES (4, N'tonmoy', N'paul', N'tonmoy', N'tonmoy@123', N'1234567', N'1', N'Pharmacist')
INSERT [dbo].[Users] ([UserID], [FirstName], [LastName], [Username], [Email], [Phone], [Password], [Role]) VALUES (5, N'kulas', N'hossain', N'kulas', N'kulas@123', N'12345', N'1', N'Admin')
INSERT [dbo].[Users] ([UserID], [FirstName], [LastName], [Username], [Email], [Phone], [Password], [Role]) VALUES (6, N'Adreta', N'mallick', N'adreta', N'adreta1@com', N'01700000000', N'1', N'Pharmacist')

SET IDENTITY_INSERT [dbo].[Users] OFF
GO
SET ANSI_PADDING ON
GO
ALTER TABLE [dbo].[Users] ADD UNIQUE NONCLUSTERED 
(
	[Username] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, IGNORE_DUP_KEY = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
GO
ALTER TABLE [dbo].[Cart] ADD  DEFAULT ((1)) FOR [Quantity]
GO
ALTER TABLE [dbo].[OrderHeaders] ADD  DEFAULT ('Pending') FOR [Status]
GO
ALTER TABLE [dbo].[OrderHeaders] ADD  DEFAULT (getdate()) FOR [OrderDate]
GO
ALTER TABLE [dbo].[Orders] ADD  DEFAULT ('Pending') FOR [Status]
GO
ALTER TABLE [dbo].[Orders] ADD  DEFAULT (getdate()) FOR [OrderDate]
GO
ALTER TABLE [dbo].[Prescriptions] ADD  DEFAULT (getdate()) FOR [UploadDate]
GO
ALTER TABLE [dbo].[Prescriptions] ADD  DEFAULT ('Pending') FOR [Status]
GO
ALTER TABLE [dbo].[Cart]  WITH CHECK ADD FOREIGN KEY([MedicineID])
REFERENCES [dbo].[Medicines] ([MedicineID])
GO
ALTER TABLE [dbo].[Cart]  WITH CHECK ADD FOREIGN KEY([UserID])
REFERENCES [dbo].[Users] ([UserID])
GO
ALTER TABLE [dbo].[OrderHeaders]  WITH CHECK ADD FOREIGN KEY([UserID])
REFERENCES [dbo].[Users] ([UserID])
GO
ALTER TABLE [dbo].[OrderItems]  WITH CHECK ADD FOREIGN KEY([OrderHeaderID])
REFERENCES [dbo].[OrderHeaders] ([OrderHeaderID])
GO
ALTER TABLE [dbo].[Orders]  WITH CHECK ADD FOREIGN KEY([UserID])
REFERENCES [dbo].[Users] ([UserID])
GO
ALTER TABLE [dbo].[Prescriptions]  WITH CHECK ADD FOREIGN KEY([UserID])
REFERENCES [dbo].[Users] ([UserID])
GO
USE [master]
GO
ALTER DATABASE [PharmacyDB] SET  READ_WRITE 
GO
```

> **Note:** The `ImagePath` values in the Medicines and Prescriptions insert statements have been left blank intentionally. After running the script, use the Admin panel to upload medicine images from your local machine.

---

## 📄 License

This project is for educational purposes.

---

> Built with ❤️ using C# Windows Forms — Pharmacy © 2026
