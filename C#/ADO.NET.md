# Complete Guide to ADO.NET

**ADO.NET (Active Data Object .NET)** is Microsoft's data access technology that lets .NET applications connect to databases (SQL Server, Oracle, etc.), run queries, and manage data.

**Creator:** Developed by Microsoft as part of the .NET Framework
**Purpose:** Unified data access for various database systems
**Current Status:** Core technology for data-driven .NET applications

---

## 1. Introduction to ADO.NET

### What is ADO.NET?

ADO.NET is a set of classes that provides data access services for .NET applications. It allows you to:
- Connect to databases
- Execute SQL queries
- Retrieve and manipulate data
- Work offline with cached data
- Synchronize data back to the database

### Two Ways to Work with Data

#### Connected Mode
- **Direct, live connection** to the database
- Data retrieved on-demand
- Connection remains open during operations
- Lower memory usage for large datasets
- Higher latency due to network communication

#### Disconnected Mode
- **Data copied to memory** for offline work
- Connection opens, retrieves data, then closes
- Applications work with in-memory data
- Higher performance for read operations
- Data is synchronized back when needed

### Core Components

- **Connection** - Links your application to the database
- **Command** - Executes queries (SELECT, INSERT, UPDATE, DELETE)
- **DataSet** - Stores data in memory (like a mini offline database)
- **DataReader** - Provides fast, forward-only read access to data
- **DataAdapter** - Bridges between DataSet and the database

### Key Features

 - **Interoperability** - Uses XML for data exchange
 - **Maintainability** - Separates data logic from UI
 - **Performance** - Works offline (disconnected), reducing database load
 - **Scalability** - Doesn't hold database connections long, so more users can connect
 - **Database Agnostic** - Same code works for different databases (Oracle, SQL Server, etc.) - just change the connection string!

---

## 2. Connection Steps (4-Step Process)

### Step 1: Create and Open Local DB Connection

```csharp
SqlConnection conn = new SqlConnection("ConnString");
conn.Open();
```

**Connection String Format:**
```
"Data Source=ServerName,Port;Initial Catalog=DatabaseName;User ID=username;Password=password;Encrypt=False;"
```

### Step 2: Load and Pass SQL Query

```csharp
SqlCommand cmd = new SqlCommand(Query, conn);  // DML + DQL
```

The query can be:
- **DQL (Data Query Language):** SELECT
- **DML (Data Manipulation Language):** INSERT, UPDATE, DELETE
- **Stored Procedure:** EXEC ProcedureName

### Step 3: Execute SQL Query

```csharp
// For DML operations (INSERT, UPDATE, DELETE)
int rowsAffected = cmd.ExecuteNonQuery();  // Returns number of rows affected

// For SELECT queries
SqlDataReader sdr = cmd.ExecuteReader();
if (sdr.HasRows)
{
    while (sdr.Read())
    {
        // Access data: sdr["ColumnName"] or sdr[index]
    }
}
sdr.Close();
```

### Step 4: Close the Connection

```csharp
conn.Close();
```

---

## 3. Basic Example: Employee Management (Simple)

### Database Setup

```sql
CREATE DATABASE DecBatch2025;
USE DecBatch2025;

CREATE TABLE Emp(
    eid INT PRIMARY KEY IDENTITY,
    ename VARCHAR(20),
    esalary DECIMAL(10,2),
    enetsalary DECIMAL(10,2)
);

CREATE PROC AddEmp
    @ename VARCHAR(20),
    @esalary DECIMAL(10,2)
AS
BEGIN
    DECLARE @enetsalary DECIMAL(10,2);
    SET @enetsalary = @esalary - (@esalary * 0.1);
    INSERT INTO emp VALUES(@ename, @esalary, @enetsalary);
END
```

### Employee Class Implementation

```csharp
using System;
using System.Data.SqlClient;

namespace DecBatch2025
{
    internal class Employee
    {
        SqlConnection conn;
        
        public Employee()
        {
            conn = new SqlConnection("Data Source=172.28.191.177,1433;Initial Catalog=DecBatch2025;Persist Security Info=True;User ID=sa;Password=Sa@123456;Encrypt=False;");
            conn.Open();
        }

        public void SaveEmp()
        {
            string ename;
            double esalary;

            Console.Write("Enter Name: ");
            ename = Console.ReadLine();
            Console.Write("Enter Salary: ");
            esalary = double.Parse(Console.ReadLine());

            string q = $"exec AddEmp '{ename}', {esalary}";
            SqlCommand cmd = new SqlCommand(q, conn);

            cmd.ExecuteNonQuery();
            Console.WriteLine("Employee Added Successfully");
        }

        public void FetchEmp()
        {
            string q = "SELECT * FROM emp";
            SqlCommand cmd = new SqlCommand(q, conn);
            SqlDataReader sdr = cmd.ExecuteReader();
            
            while (sdr.Read())
            {
                Console.WriteLine($"ID: {sdr["eid"]} \nName: {sdr["ename"]} \nSalary: {sdr["esalary"]} \nNet Salary: {sdr["enetsalary"]}");
            }
            sdr.Close();
        }
    }
}
```

### Main Program

```csharp
using DecBatch2025;

class Program
{
    static void Main(string[] args)
    {
        Employee obj = new Employee();
        obj.SaveEmp();
        obj.FetchEmp();
    }
}
```

### Output

```
Enter Name: kiran
Enter Salary: 100000
Employee Added Successfully

ID: 1
Name: kiran
Salary: 100000.00
Net Salary: 90000.00
```

---

## 4. Advanced Example: Complete CRUD Operations

### Database Setup with Stored Procedure

```sql
CREATE DATABASE DecBatch2025;
USE DecBatch2025;

CREATE TABLE Emp(
    eid INT PRIMARY KEY IDENTITY,
    ename VARCHAR(20),
    esalary DECIMAL(10,2),
    enetsalary DECIMAL(10,2)
);

CREATE PROC EmpManagement
    @eid INT = NULL,
    @ename VARCHAR(20) = NULL,
    @esalary DECIMAL(10,2) = NULL,
    @choice INT
AS
BEGIN
    IF (@choice = 1)
    BEGIN
        -- Add Employee
        DECLARE @enetsalary DECIMAL(10,2);
        SET @enetsalary = @esalary - (@esalary * 0.1);
        INSERT INTO emp VALUES(@ename, @esalary, @enetsalary);
    END
    ELSE IF (@choice = 2)
    BEGIN
        -- Fetch All Employees
        SELECT * FROM emp;
    END
    ELSE IF (@choice = 3)
    BEGIN
        -- Update Both Name and Salary
        SET @enetsalary = @esalary - (@esalary * 0.1);
        UPDATE emp SET ename = @ename, esalary = @esalary, enetsalary = @enetsalary WHERE eid = @eid;
    END
    ELSE IF (@choice = 4)
    BEGIN
        -- Search Employee by Name
        SELECT * FROM emp WHERE ename LIKE '%' + @ename + '%';
    END
    ELSE IF (@choice = 5)
    BEGIN
        -- Update Name Only
        UPDATE emp SET ename = @ename WHERE eid = @eid;
    END
    ELSE IF (@choice = 6)
    BEGIN
        -- Update Salary Only
        SET @enetsalary = @esalary - (@esalary * 0.1);
        UPDATE emp SET esalary = @esalary, enetsalary = @enetsalary WHERE eid = @eid;
    END
    ELSE IF (@choice = 7)
    BEGIN
        -- Delete Employee
        DELETE FROM emp WHERE eid = @eid;
    END
END
```

### Complete Employee Class with CRUD

```csharp
using System;
using System.Data.SqlClient;

namespace DecBatch2025
{
    internal class Employee
    {
        SqlConnection conn;
        
        public Employee()
        {
            conn = new SqlConnection("Data Source=172.28.191.177,1433;Initial Catalog=DecBatch2025;Persist Security Info=True;User ID=sa;Password=Sa@123456;Encrypt=False;");
            conn.Open();
        }

        /// <summary>
        /// CREATE: Add a new employee
        /// </summary>
        public void SaveEmp()
        {
            string ename;
            double esalary;

            Console.Write("\nEnter Name: ");
            ename = Console.ReadLine();
            Console.Write("Enter Salary: ");
            esalary = double.Parse(Console.ReadLine());

            string q = $"exec EmpManagement @ename = '{ename}', @esalary = '{esalary}', @choice = 1";
            SqlCommand cmd = new SqlCommand(q, conn);

            cmd.ExecuteNonQuery();
            Console.WriteLine("Employee Added Successfully");
        }

        /// <summary>
        /// READ: Fetch all employees
        /// </summary>
        public void FetchEmp()
        {
            string q = "exec EmpManagement @choice = 2";
            SqlCommand cmd = new SqlCommand(q, conn);
            SqlDataReader sdr = cmd.ExecuteReader();

            Console.WriteLine("\n--- All Employees ---");
            while (sdr.Read())
            {
                Console.WriteLine($"\nID: {sdr["eid"]} | Name: {sdr["ename"]} | Salary: {sdr["esalary"]} | Net Salary: {sdr["enetsalary"]}");
            }
            sdr.Close();
        }

        /// <summary>
        /// UPDATE: Modify employee information
        /// </summary>
        public void UpdateEmp()
        {
            string ename;
            double esalary;
            int eid;
            int choice;

            do
            {
                Console.WriteLine("\n--- Update Options ---");
                Console.WriteLine("1. Update Employee Name");
                Console.WriteLine("2. Update Employee Salary");
                Console.WriteLine("3. Update Both");
                Console.WriteLine("4. Exit");
                Console.Write("Enter your choice: ");
                choice = int.Parse(Console.ReadLine());

                switch (choice)
                {
                    case 1:
                        Console.Write("\nEnter ID: ");
                        eid = int.Parse(Console.ReadLine());
                        Console.Write("Enter New Name: ");
                        ename = Console.ReadLine();

                        string q1 = $"exec EmpManagement @eid = {eid}, @ename = '{ename}', @choice = 5";
                        SqlCommand cmd1 = new SqlCommand(q1, conn);
                        cmd1.ExecuteNonQuery();
                        Console.WriteLine("Name Updated Successfully");
                        break;

                    case 2:
                        Console.Write("\nEnter ID: ");
                        eid = int.Parse(Console.ReadLine());
                        Console.Write("Enter New Salary: ");
                        esalary = double.Parse(Console.ReadLine());

                        string q2 = $"exec EmpManagement @eid = {eid}, @esalary = '{esalary}', @choice = 6";
                        SqlCommand cmd2 = new SqlCommand(q2, conn);
                        cmd2.ExecuteNonQuery();
                        Console.WriteLine("Salary Updated Successfully");
                        break;

                    case 3:
                        Console.Write("\nEnter ID: ");
                        eid = int.Parse(Console.ReadLine());
                        Console.Write("Enter New Name: ");
                        ename = Console.ReadLine();
                        Console.Write("Enter New Salary: ");
                        esalary = double.Parse(Console.ReadLine());

                        string q3 = $"exec EmpManagement @eid = {eid}, @ename = '{ename}', @esalary = '{esalary}', @choice = 3";
                        SqlCommand cmd3 = new SqlCommand(q3, conn);
                        cmd3.ExecuteNonQuery();
                        Console.WriteLine("Employee Updated Successfully");
                        break;

                    case 4:
                        Console.WriteLine("Exiting Update Menu...");
                        break;

                    default:
                        Console.WriteLine("Invalid choice!");
                        break;
                }
            } while (choice != 4);
        }

        /// <summary>
        /// DELETE: Remove an employee
        /// </summary>
        public void DeleteEmp()
        {
            int eid;

            Console.Write("\nEnter Employee ID to Delete: ");
            eid = int.Parse(Console.ReadLine());

            string q = $"exec EmpManagement @eid = {eid}, @choice = 7";
            SqlCommand cmd = new SqlCommand(q, conn);

            cmd.ExecuteNonQuery();
            Console.WriteLine("Employee Deleted Successfully");
        }

        /// <summary>
        /// SEARCH: Find employees by name
        /// </summary>
        public void SearchEmp()
        {
            string ename;

            Console.Write("\nEnter Employee Name to Search: ");
            ename = Console.ReadLine();

            string q = $"exec EmpManagement @ename = '{ename}', @choice = 4";
            SqlCommand cmd = new SqlCommand(q, conn);
            SqlDataReader sdr = cmd.ExecuteReader();

            Console.WriteLine("\n--- Search Results ---");
            bool found = false;
            while (sdr.Read())
            {
                found = true;
                Console.WriteLine($"\nID: {sdr["eid"]} | Name: {sdr["ename"]} | Salary: {sdr["esalary"]} | Net Salary: {sdr["enetsalary"]}");
            }
            if (!found)
            {
                Console.WriteLine("No employees found with that name.");
            }
            sdr.Close();
        }
    }
}
```

### Main Program with Menu System

```csharp
using System;
using DecBatch2025;

class Program
{
    static void Main(string[] args)
    {
        Employee emp = new Employee();
        int choice;

        do
        {
            Console.WriteLine("\n====== Employee Management System ======");
            Console.WriteLine("1. Add Employee");
            Console.WriteLine("2. View All Employees");
            Console.WriteLine("3. Update Employee");
            Console.WriteLine("4. Delete Employee");
            Console.WriteLine("5. Search Employee");
            Console.WriteLine("6. Exit");
            Console.Write("Enter your choice: ");
            choice = int.Parse(Console.ReadLine());

            switch (choice)
            {
                case 1:
                    emp.SaveEmp();
                    break;
                case 2:
                    emp.FetchEmp();
                    break;
                case 3:
                    emp.UpdateEmp();
                    break;
                case 4:
                    emp.DeleteEmp();
                    break;
                case 5:
                    emp.SearchEmp();
                    break;
                case 6:
                    Console.WriteLine("Thank you! Exiting...");
                    break;
                default:
                    Console.WriteLine("Invalid choice! Try again.");
                    break;
            }
        } while (choice != 6);
    }
}
```

### Sample Output

```
====== Employee Management System ======
1. Add Employee
2. View All Employees
3. Update Employee
4. Delete Employee
5. Search Employee
6. Exit
Enter your choice: 1

Enter Name: karan
Enter Salary: 100000
Employee Added Successfully

====== Employee Management System ======
1. Add Employee
2. View All Employees
3. Update Employee
4. Delete Employee
5. Search Employee
6. Exit
Enter your choice: 2

--- All Employees ---

ID: 8 | Name: kiran | Salary: 500000.00 | Net Salary: 450000.00
ID: 9 | Name: karan | Salary: 100000.00 | Net Salary: 90000.00

====== Employee Management System ======
1. Add Employee
2. View All Employees
3. Update Employee
4. Delete Employee
5. Search Employee
6. Exit
Enter your choice: 5

Enter Employee Name to Search: karan

--- Search Results ---

ID: 9 | Name: karan | Salary: 100000.00 | Net Salary: 90000.00

====== Employee Management System ======
1. Add Employee
2. View All Employees
3. Update Employee
4. Delete Employee
5. Search Employee
6. Exit
Enter your choice: 6

Thank you! Exiting...
```

---

## 5. Best Practices for ADO.NET

###  DO

- **Use Parameterized Queries** - Prevent SQL injection attacks
- **Close Connections** - Always close connections in finally blocks or use `using` statements
- **Use Connection Pooling** - Reuse connections for better performance
- **Validate User Input** - Always validate and sanitize data before database operations
- **Use Stored Procedures** - For complex queries and better performance
- **Implement Error Handling** - Use try-catch-finally blocks

###  DON'T

- **String Concatenation in Queries** - Vulnerable to SQL injection
- **Keep Connections Open** - Wastes resources and reduces scalability
- **Ignore Exceptions** - Always handle and log errors
- **Hardcode Connection Strings** - Use configuration files or environment variables
- **Trust User Input** - Always validate before using in queries

### Using Statement (Best Practice)

```csharp
using (SqlConnection conn = new SqlConnection(connString))
{
    conn.Open();
    using (SqlCommand cmd = new SqlCommand(query, conn))
    {
        // Execute command
    }
} // Connection automatically closed and disposed
```

---

## 6. Key Components Summary

### SqlConnection
- Establishes a connection to the database
- Methods: Open(), Close(), Dispose()
- Properties: ConnectionString, State

### SqlCommand
- Executes SQL statements or stored procedures
- Methods: ExecuteNonQuery(), ExecuteReader(), ExecuteScalar()
- Properties: CommandText, CommandType, Connection

### SqlDataReader
- Provides fast, forward-only, read-only access
- Methods: Read(), Close(), Dispose()
- Best for: Large datasets, streaming data

### SqlDataAdapter
- Acts as a bridge between DataSet and database
- Methods: Fill(), Update()
- Best for: Disconnected mode, offline operations

### DataSet
- In-memory representation of data
- Can contain multiple tables (DataTable objects)
- Best for: Complex data operations, multiple tables

---

