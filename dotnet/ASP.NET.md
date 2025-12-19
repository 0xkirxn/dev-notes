# Complete Guide to ASP.NET Web Forms

**ASP.NET Web Forms** is Microsoft's framework for building interactive web applications with graphical user interfaces. Unlike C# Console Applications that use command-line interfaces, ASP.NET provides a robust server-side framework for creating feature-rich web experiences.

**Key Characteristic:** Server-side language requiring a server (like IIS - Internet Information Services provided by Visual Studio) to execute code and render pages.

**Created By:** Microsoft as an evolution of web development technologies

**Current Status:** Still widely used for enterprise applications; newer versions include ASP.NET MVC and ASP.NET Core

---

## 1. Introduction to ASP.NET and Web Forms

### What is ASP.NET Web Forms?

Unlike C# Console Applications which rely on command-line interfaces, ASP.NET allows for the creation of interactive Web Applications with a User Interface (UI). It is a server-side language, meaning it requires a server (like the default IIS server provided by Visual Studio) to execute the code.

### Evolution of Web Technologies

#### CGI (Common Gateway Interface)
- Traditional method where every single resource request required a separate request to the server
- If 1000 resources were needed, 1000 separate requests were made
- Major performance limitations

#### ASP (Active Server Pages)
- Improved performance with better resource handling
- Single file for both UI and backend logic
- Partially object-oriented approach

#### ASP.NET
- Modern evolution of ASP
- **Advantage:** Allows a single request to handle multiple resources/responses, significantly improving performance
- Uses separate files for UI (`.aspx`) and Logic (`.aspx.cs`), known as "Code Behind"
- Purely Object-Oriented architecture
- Better separation of concerns

### Client-Side Controls vs. Server-Side Controls

#### Client-Side (HTML)
- Standard HTML controls like `<input type="text">`
- Create a UI but cannot directly interact with C# backend code
- Limited integration with server logic
- Example: `<input type="text">`

#### Server-Side (ASP.NET)
- Controls from the ASP.NET Toolbox
- Must have the `runat="server"` attribute
- Allow backend logic to interact with the UI
- Example: Getting data from a TextBox on a button click
- Must be placed inside `<form runat="server">` tag

### Syntax Comparison

| HTML | ASP.NET |
|------|---------|
| `<input type="text">` | `<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>` |
| Limited backend interaction | Full C# backend integration |
| Client-side processing | Server-side processing |

**Critical Rule:** All server controls must be placed inside a `<form runat="server">` tag.

---

## 2. Page Structure and Architecture

### File Organization

ASP.NET Web Forms uses a two-file architecture for better separation of concerns:

| File | Purpose | Language |
|------|---------|----------|
| `.aspx` | Frontend/Design/User Interface | HTML + ASP.NET markup |
| `.aspx.cs` | Backend/Code Behind | C# |

The two files are linked via the `Inherits` and `CodeBehind` directives at the top of the `.aspx` page.

**Example Structure:**
```html
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Default.aspx.cs" Inherits="WebApplication1.Default" %>
```

### ASP.NET Page Life Cycle

When an ASP.NET page executes, it goes through specific stages in a defined order:

#### Lifecycle Stages

1. **Page Request** - The server checks if the page needs to be compiled or served from cache
2. **Start** - Sets request/response properties for the page
3. **Initialization** - Loads unique IDs for all controls
4. **Load** - Handles `Page_Load` events and restores control states
5. **Event Handling** - Validates and handles specific events (like Button Clicks)
6. **Rendering** - Converts Server-Side controls (ASP tags) into HTML controls so the browser can understand them
7. **Unload** - Cleanup and closing of the request

#### Event Execution Order

The specific events occur in this exact order:

```
PreInit → Init → InitComplete → PreLoad → Load → LoadComplete → PreRender → Render → Unload
```

### Page_Load vs. Event Handlers

#### Page_Load
- Runs **every time** the page loads (initial load and postbacks)
- Useful for initial setup and variable initialization
- Executes before any button click events

#### Event Handlers (e.g., Button_Click)
- Runs **only when the specific event occurs** (e.g., button clicked)
- Executes after Page_Load
- Used for user interactions

**Example:**
```csharp
protected void Page_Load(object sender, EventArgs e)
{
    // Runs every time page loads
    Label1.Text = "Initial Label";
}

protected void Button1_Click(object sender, EventArgs e)
{
    // Runs only when button is clicked
    Label1.Text = "Button Clicked";
}
``` 

---

## 3. Web Form Controls and Implementation

### Creating an ASP.NET Web Project

**Steps to Create a Project:**
1. Select **"ASP.NET Web Application (.NET Framework)"** template
2. Choose an **Empty** template or **Web Forms** template
3. Right-click the project → **Add** → **New Item** → **Web Form**
4. Name your `.aspx` page (e.g., Default.aspx)

### Working with the Toolbox

- Controls are dragged and dropped from the **Toolbox** in Design View
- If the Toolbox is empty, ensure an active Web Form is open
- All controls need an `ID` property to reference them in C# code
- All server controls need `runat="server"` attribute

### Common Web Form Controls

#### TextBox (Input Control)
Captures user text input.

```html
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
```

**Retrieving Data:**
```csharp
string name = TextBox1.Text;  // Gets input as string
int age = int.Parse(TextBox1.Text);  // Parse to integer
```

#### Button (Action Control)
Triggers events when clicked.

```html
<asp:Button ID="Button1" runat="server" Text="Submit" OnClick="Button1_Click" />
```

**Event Handler:**
```csharp
protected void Button1_Click(object sender, EventArgs e)
{
    // Code executes when button is clicked
}
```

#### Label (Display Control)
Displays text to the user (read-only).

```html
<asp:Label ID="Label1" runat="server" Text=""></asp:Label>
```

**Setting Data:**
```csharp
Label1.Text = "Hello World";
Label1.Text = $"Hello {username}";
```

#### DropDownList (Selection Control)
Allows user to select one item from a list.

```html
<asp:DropDownList ID="DropDownList1" runat="server">
    <asp:ListItem>Option 1</asp:ListItem>
    <asp:ListItem>Option 2</asp:ListItem>
</asp:DropDownList>
```

**Retrieving Data:**
```csharp
string choice = DropDownList1.SelectedValue;
string text = DropDownList1.SelectedItem.Text;
```

#### ListBox (Multiple Selection Control)
Allows selecting multiple items (requires `SelectionMode="Multiple"`).

```html
<asp:ListBox ID="ListBox1" runat="server" SelectionMode="Multiple"></asp:ListBox>
```

**Difference from DropDownList:**
- DropDownList allows **single selection only**
- ListBox allows **multiple selections** via Ctrl+Click

#### Image (Display Control)
Displays images on the page.

```html
<asp:Image ID="Image1" runat="server" ImageUrl="~/Images/pic.png" />
```

#### FileUpload (Input Control)
Allows users to upload files.

```html
<asp:FileUpload ID="FileUpload1" runat="server" />
```

### Example: Employee Form

A practical example showing how to collect employee information and display it.

**Frontend (.aspx):**
```html
<form runat="server">
    <asp:Label Text="Name:" runat="server"></asp:Label>
    <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
    
    <asp:Label Text="ID:" runat="server"></asp:Label>
    <asp:TextBox ID="TextBox2" runat="server"></asp:TextBox>
    
    <asp:Label Text="Department:" runat="server"></asp:Label>
    <asp:DropDownList ID="DropDownList1" runat="server">
        <asp:ListItem>IT</asp:ListItem>
        <asp:ListItem>HR</asp:ListItem>
        <asp:ListItem>Finance</asp:ListItem>
    </asp:DropDownList>
    
    <asp:Label Text="Salary:" runat="server"></asp:Label>
    <asp:TextBox ID="TextBox3" runat="server"></asp:TextBox>
    
    <asp:Button ID="Button1" runat="server" Text="Submit" OnClick="Button1_Click" />
    
    <asp:Label ID="Label1" runat="server"></asp:Label>
    <asp:Label ID="Label2" runat="server"></asp:Label>
    <asp:Label ID="Label3" runat="server"></asp:Label>
    <asp:Label ID="Label4" runat="server"></asp:Label>
</form>
```

**Backend (.aspx.cs):**
```csharp
protected void Button1_Click(object sender, EventArgs e)
{
    // Fetching String Data
    string name = TextBox1.Text;

    // Fetching and Parsing Integer Data
    // Type casting is required because TextBox.Text returns a string
    int id = int.Parse(TextBox2.Text);

    // Fetching DropDown Data
    string department = DropDownList1.SelectedValue;

    // Fetching and Parsing Double Data
    double salary = double.Parse(TextBox3.Text);

    // Displaying Logic (using String Interpolation and Concatenation)
    Label1.Text = "Name: " + name;
    Label2.Text = $"ID: {id}";
    Label3.Text = $"Department: {department}";
    Label4.Text = $"Salary: {salary}";
}
```

---

## 4. Web Form Logic Implementation and Rules

### Critical Rules for Web Forms

#### Rule 1: Controls Must Be Inside Form Tag
All server controls **must** be placed inside the `<form runat="server">` tag. Placing them outside results in a runtime error.

```html
<form runat="server">
    <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
    <asp:Button ID="Button1" runat="server" Text="Click Me" />
</form>
```

#### Rule 2: Only One Form Tag Per Page
An ASP.NET page can have **only one** `<form runat="server">` tag. You **cannot** have multiple server-side forms on one page.

**Handling Multiple Sections:**
If you need to handle different logical sections (e.g., Addition section vs. Subtraction section), keep them in the same form but use different Buttons with unique event handlers.

```csharp
protected void ButtonAdd_Click(object sender, EventArgs e)
{
    // Handle addition logic
}

protected void ButtonSubtract_Click(object sender, EventArgs e)
{
    // Handle subtraction logic
}
```

### Logic Implementation Examples

#### Example 1: Simple Addition

**Scenario:** Two TextBoxes for input, one Button to calculate the sum.

**Frontend:**
```html
<form runat="server">
    <asp:TextBox ID="TextBox1" runat="server" Placeholder="Enter first number"></asp:TextBox>
    <asp:TextBox ID="TextBox2" runat="server" Placeholder="Enter second number"></asp:TextBox>
    <asp:Button ID="Button_Add" runat="server" Text="Add" OnClick="Button_Add_Click" />
    <asp:Label ID="LabelResult" runat="server"></asp:Label>
</form>
```

**Backend:**
```csharp
protected void Button_Add_Click(object sender, EventArgs e)
{
    int a = int.Parse(TextBox1.Text);
    int b = int.Parse(TextBox2.Text);
    int c = a + b;

    // Display result
    LabelResult.Text = $"Addition Result: {c}";
}
```

#### Example 2: Calculator with Conditionals

**Scenario:** Using a DropDownList to select an operator (+, -, *, /) and performing appropriate calculation.

**Frontend:**
```html
<form runat="server">
    <asp:TextBox ID="TextBox1" runat="server" Placeholder="Number 1"></asp:TextBox>
    <asp:TextBox ID="TextBox2" runat="server" Placeholder="Number 2"></asp:TextBox>
    
    <asp:DropDownList ID="DropDownList1" runat="server">
        <asp:ListItem>+</asp:ListItem>
        <asp:ListItem>-</asp:ListItem>
        <asp:ListItem>*</asp:ListItem>
        <asp:ListItem>/</asp:ListItem>
    </asp:DropDownList>
    
    <asp:Button ID="Button_Result" runat="server" Text="Calculate" OnClick="Button_Result_Click" />
    <asp:Label ID="LabelResult" runat="server"></asp:Label>
</form>
```

**Backend:**
```csharp
protected void Button_Result_Click(object sender, EventArgs e)
{
    int a = int.Parse(TextBox1.Text);
    int b = int.Parse(TextBox2.Text);
    string choice = DropDownList1.SelectedValue;  // Get operator
    int result = 0;

    // Logic using .Equals() for string comparison
    if (choice.Equals("+"))
    {
        result = a + b;
    }
    else if (choice.Equals("-"))
    {
        result = a - b;
    }
    else if (choice.Equals("*"))
    {
        result = a * b;
    }
    else if (choice.Equals("/"))
    {
        if (b != 0)
            result = a / b;
        else
            LabelResult.Text = "Cannot divide by zero!";
    }

    LabelResult.Text = $"Result: {result}";
}
```

#### Example 3: Sum of Digits (Using Loops)

**Scenario:** User enters a number, and we calculate the sum of all its digits.

**Example:** 123 → 1+2+3 = 6

**Frontend:**
```html
<form runat="server">
    <asp:TextBox ID="TextBoxNumber" runat="server" Placeholder="Enter a number"></asp:TextBox>
    <asp:Button ID="Button_Sum" runat="server" Text="Calculate Sum" OnClick="Button_Sum_Click" />
    <asp:Label ID="LabelResult" runat="server"></asp:Label>
</form>
```

**Backend:**
```csharp
protected void Button_Sum_Click(object sender, EventArgs e)
{
    int n = int.Parse(TextBoxNumber.Text);
    int sum = 0;
    int remainder;

    // Standard While Loop Logic (works exactly like C# console apps)
    while (n > 0)
    {
        remainder = n % 10;      // Get the last digit
        sum = sum + remainder;   // Add to sum
        n = n / 10;              // Remove the last digit
    }

    LabelResult.Text = $"Sum of digits: {sum}";
}
```

---

## 5. Database Integration with ADO.NET

### Web.config Configuration

To connect your ASP.NET Web Forms application to a database, add a connection string to the `Web.config` file:

```xml
<configuration>
  <connectionStrings>
    <add name="dbconn" connectionString="Data Source=172.28.191.177,1433;Initial Catalog=DecBatch2025;Persist Security Info=True;User ID=sa;Password=Sa@123456;Encrypt=False;"/>
  </connectionStrings>
</configuration>
```

**Key Points:**
- Store connection strings in `Web.config` for security and maintainability
- Use `ConfigurationManager` to retrieve the connection string in your code
- Never hardcode credentials in your source code

### Retrieving Connection String from Web.config

```csharp
using System.Configuration;

string connectionString = ConfigurationManager.ConnectionStrings["dbconn"].ConnectionString;
```

### Required Namespaces

```csharp
using System.Data;
using System.Data.SqlClient;
using System.Configuration;
```

---

## 6. Authentication System: SignUp, SignIn, and Session Management

### Database Setup

Before implementing authentication, create the necessary database objects:

```sql
CREATE DATABASE DecBatch2025;
USE DecBatch2025;

CREATE TABLE Auth(
id int primary key identity,
email varchar(40) ,
username varchar(20),
pass varchar(20),
);

CREATE proc SignUp
@email varchar(40),
@username varchar(20),
@pass varchar(20)
AS
BEGIN 
	INSERT INTO Auth VALUES (@email,@username,@pass);
end

ALTER proc SignIn
@var varchar(40),
@pass varchar(20)
AS
BEGIN 
	SELECT * FROM Auth WHERE (email = @var OR username = @var) AND pass = @pass;
end

ALTER PROC SignUp
@email varchar(40),
@username varchar(20),
@pass varchar(20)
AS
BEGIN 
    IF EXISTS (SELECT 1 FROM Auth WHERE email = @email OR username = @username)
    BEGIN
        RAISERROR('User already exists!', 16, 1);
        RETURN;
    END
    INSERT INTO Auth VALUES (@email, @username, @pass);
END
```

### SignUp Page Implementation

**Purpose:** Register new users into the system.

**Frontend (SignUp.aspx):**
```html
<form runat="server">
    <asp:Label Text="Username:" runat="server"></asp:Label>
    <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
    
    <asp:Label Text="Email:" runat="server"></asp:Label>
    <asp:TextBox ID="TextBox2" runat="server" TextMode="Email"></asp:TextBox>
    
    <asp:Label Text="Password:" runat="server"></asp:Label>
    <asp:TextBox ID="TextBox3" runat="server" TextMode="Password"></asp:TextBox>
    
    <asp:Button ID="Button1" runat="server" Text="Register" OnClick="Button1_Click" />
</form>
```

**Backend (SignUp.aspx.cs):**
```csharp
public partial class Signup : System.Web.UI.Page
{
    SqlConnection conn;
    
    protected void Page_Load(object sender, EventArgs e)
    {
        string str = ConfigurationManager.ConnectionStrings["dbconn"].ConnectionString;
        conn = new SqlConnection(str);
        conn.Open();
    }

    protected void Button1_Click(object sender, EventArgs e)
    {
        try
        {
            string q = $"exec SignUp '{TextBox1.Text}','{TextBox2.Text}','{TextBox3.Text}'";
            SqlCommand cmd = new SqlCommand(q, conn);
            cmd.ExecuteNonQuery();
            
            // Show success message
            Response.Write("<script>alert('User Registered Successfully!')</script>");
        }
        catch (SqlException ex)
        {
            // Show error message
            Response.Write("<script>alert('" + ex.Message + "')</script>");
        }
    }
}
```

### SignIn Page Implementation

**Purpose:** Authenticate users and create sessions.

**Frontend (Login.aspx):**
```html
<form runat="server">
    <asp:Label Text="Username or Email:" runat="server"></asp:Label>
    <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
    
    <asp:Label Text="Password:" runat="server"></asp:Label>
    <asp:TextBox ID="TextBox2" runat="server" TextMode="Password"></asp:TextBox>
    
    <asp:Button ID="Button1" runat="server" Text="Sign In" OnClick="Button1_Click" />
</form>
```

**Backend (Login.aspx.cs):**
```csharp
public partial class Login : System.Web.UI.Page
{
    SqlConnection conn;
    
    protected void Page_Load(object sender, EventArgs e)
    {
        string str = ConfigurationManager.ConnectionStrings["dbconn"].ConnectionString;
        conn = new SqlConnection(str);
        conn.Open();
    }

    protected void Button1_Click(object sender, EventArgs e)
    {
        string username_or_email = TextBox1.Text;
        string password = TextBox2.Text;
        
        string q = $"exec SignIn '{username_or_email}','{password}'";
        SqlCommand cmd = new SqlCommand(q, conn);
        SqlDataReader rdr = cmd.ExecuteReader();
        
        if (rdr.HasRows)
        {
            while (rdr.Read())
            {
                // Verify credentials
                if ((rdr["username"].Equals(username_or_email) || rdr["email"].Equals(username_or_email)) 
                    && rdr["pass"].Equals(password))
                {
                    // Create session for authenticated user
                    Session["ref"] = rdr["username"].ToString();
                    Response.Redirect("Welcome.aspx");
                }
            }
        }
        else
        {
            Response.Write("<script>alert('Invalid Credentials!!')</script>");
        }
        
        rdr.Close();
    }
}
```

### Welcome Page with Session Management

**Purpose:** Display authenticated user information and manage logout.

**Frontend (Welcome.aspx):**
```html
<form runat="server">
    <asp:Label Text="Welcome, "></asp:Label>
    <asp:Label ID="Label1" runat="server"></asp:Label>
    
    <asp:Button ID="Button1" runat="server" Text="Logout" OnClick="Button1_Click" />
</form>
```

**Backend (Welcome.aspx.cs):**
```csharp
public partial class Welcome : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        // Check if user is logged in
        if (Session["ref"] != null)
        {
            // Display username
            Label1.Text = Session["ref"].ToString();
        }
        else
        {
            // Redirect to login if not authenticated
            Response.Write("<script>alert('Need To Login!!');window.location.href='Login.aspx';</script>");
        }
    }

    protected void Button1_Click(object sender, EventArgs e)
    {
        // Logout: Destroy session
        Session.Abandon();              // Destroy entire session
        Session.Remove("ref");          // Remove specific session variable
        // Session.Clear();             // Alternative: remove all session variables
        
        Response.Redirect("Login.aspx");
    }
}
```

### Session Management Methods

| Method | Purpose | Usage |
|--------|---------|-------|
| `Session["key"] = value` | Create/set session variable | Store user data |
| `Session["key"]` | Retrieve session variable | Access stored data |
| `Session["key"] != null` | Check if session exists | Verify authentication |
| `Session.Remove("key")` | Remove specific session | Clear individual data |
| `Session.Clear()` | Remove all sessions | Clear all stored data |
| `Session.Abandon()` | Destroy entire session | Complete logout |

---
