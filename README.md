# 🎯 C# Properties & Methods Project

## Lesson Snapshot
Build a smart bank account system that protects money and tracks transactions automatically! (Ages 8-18)

## Folder & File Map
```
CSharp-Lesson-Six/
├── .git/
├── .gitignore
├── CSharp-Lesson-Six.csproj
└── Program.cs
```

## How to use the code snippets
Each step below shows the **complete contents** of `Program.cs` after you finish that step. When a step says "replace your `Program.cs` with this", select all (Ctrl+A / Cmd+A) inside `Program.cs`, delete it, then paste the new code. That keeps you from ending up with two `Main` methods or leftover code from earlier steps.

## Step-by-Step Build Guide

### 1. Fork and Clone the Repository ✅
- **What to do**: Go to [https://github.com/PhillyCoderDojo/CSharp-Lesson-Six](https://github.com/PhillyCoderDojo/CSharp-Lesson-Six) → Click "Fork" → Open GitHub Desktop → Clone your fork
- **File(s) touched**: Creating project folder
- **Code snippet**: None
- **Why it matters**: Get your workspace for advanced class features
- **Git command**: `git clone https://github.com/YOUR-USERNAME/CSharp-Lesson-Six.git`

### 2. Open Project in Rider ✅
- **What to do**: Open Rider → File → Open → Select your cloned folder → Click OK
- **File(s) touched**: Loading project
- **Code snippet**: None
- **Why it matters**: Time to master properties and methods!
- **Git command**: None

### 3. Create Basic Account Class 🏦
- **What to do**: Replace your `Program.cs` with the code below. It adds a simple `BankAccount` class with two public fields and a constructor.
- **File(s) touched**: Program.cs
- **Code snippet** (full file):
```csharp
namespace CSharp_Lesson_Six;

class BankAccount
{
    public string Owner;
    public double Balance;

    public BankAccount(string owner, double startingBalance)
    {
        Owner = owner;
        Balance = startingBalance;
        Console.WriteLine($"Account created for {Owner} with ${Balance}");
    }
}

class Program
{
    static void Main(string[] args)
    {
        BankAccount account = new BankAccount("Alex", 100.00);
        Console.WriteLine($"{account.Owner} has ${account.Balance}");
    }
}
```
- **Why it matters**: Start with simple fields before adding protection
- **Git command**: `git add . && git commit -m "Create basic BankAccount class"`

### 4. Add Methods for Account Actions 💰
- **What to do**: Replace your `Program.cs` with the version below. The account can now `Deposit` and `Withdraw`, and `Main` calls both.
- **File(s) touched**: Program.cs
- **Code snippet** (full file):
```csharp
namespace CSharp_Lesson_Six;

class BankAccount
{
    public string Owner;
    public double Balance;

    public BankAccount(string owner, double startingBalance)
    {
        Owner = owner;
        Balance = startingBalance;
        Console.WriteLine($"Account created for {Owner} with ${Balance}");
    }

    public void Deposit(double amount)
    {
        if (amount > 0)
        {
            Balance += amount;
            Console.WriteLine($"Deposited ${amount}. New balance: ${Balance}");
        }
        else
        {
            Console.WriteLine("Deposit amount must be positive!");
        }
    }

    public void Withdraw(double amount)
    {
        if (amount > 0 && amount <= Balance)
        {
            Balance -= amount;
            Console.WriteLine($"Withdrew ${amount}. New balance: ${Balance}");
        }
        else
        {
            Console.WriteLine("Invalid withdrawal amount!");
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        BankAccount account = new BankAccount("Alex", 100.00);
        account.Deposit(50.00);
        account.Withdraw(25.00);
        Console.WriteLine($"{account.Owner} now has ${account.Balance}");
    }
}
```
- **Why it matters**: Methods control how data changes
- **Git command**: `git add . && git commit -m "Add Deposit and Withdraw methods"`

### 5. Convert Fields to Properties 🔒
- **What to do**: Replace your `Program.cs` with the version below. `Owner` is now an auto-property and `Balance` has a backing field with a **private setter** — so only `BankAccount` methods can change the balance.
- **File(s) touched**: Program.cs
- **Code snippet** (full file):
```csharp
namespace CSharp_Lesson_Six;

class BankAccount
{
    private double _balance;
    public string Owner { get; set; }

    public double Balance
    {
        get { return _balance; }
        private set { _balance = value; }
    }

    public BankAccount(string owner, double startingBalance)
    {
        Owner = owner;
        _balance = startingBalance >= 0 ? startingBalance : 0;
        Console.WriteLine($"Account created for {Owner} with ${Balance}");
    }

    public void Deposit(double amount)
    {
        if (amount > 0)
        {
            Balance += amount;
            Console.WriteLine($"Deposited ${amount}. New balance: ${Balance}");
        }
        else
        {
            Console.WriteLine("Deposit amount must be positive!");
        }
    }

    public void Withdraw(double amount)
    {
        if (amount > 0 && amount <= Balance)
        {
            Balance -= amount;
            Console.WriteLine($"Withdrew ${amount}. New balance: ${Balance}");
        }
        else
        {
            Console.WriteLine("Invalid withdrawal amount!");
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        BankAccount account = new BankAccount("Alex", 100.00);
        account.Deposit(50.00);
        account.Withdraw(25.00);
        Console.WriteLine($"{account.Owner} now has ${account.Balance}");
    }
}
```
- **Why it matters**: Properties control who can read/write data
- **Git command**: `git add . && git commit -m "Convert balance to protected property"`

### 6. Add Advanced Property Validation 🛡️
- **What to do**: Replace your `Program.cs` with the version below. `Owner` is now a full property with a backing field `_owner`, and the setter cleans up empty/whitespace names.
- **File(s) touched**: Program.cs
- **Code snippet** (full file):
```csharp
namespace CSharp_Lesson_Six;

class BankAccount
{
    private string _owner;
    private double _balance;

    public string Owner
    {
        get { return _owner; }
        set
        {
            if (string.IsNullOrWhiteSpace(value))
            {
                Console.WriteLine("Owner name cannot be empty!");
                _owner = "Unknown Owner";
            }
            else
            {
                _owner = value.Trim();
            }
        }
    }

    public double Balance
    {
        get { return _balance; }
        private set { _balance = value; }
    }

    public BankAccount(string owner, double startingBalance)
    {
        Owner = owner;
        _balance = startingBalance >= 0 ? startingBalance : 0;
        Console.WriteLine($"Account created for {Owner} with ${Balance}");
    }

    public void Deposit(double amount)
    {
        if (amount > 0)
        {
            Balance += amount;
            Console.WriteLine($"Deposited ${amount}. New balance: ${Balance}");
        }
        else
        {
            Console.WriteLine("Deposit amount must be positive!");
        }
    }

    public void Withdraw(double amount)
    {
        if (amount > 0 && amount <= Balance)
        {
            Balance -= amount;
            Console.WriteLine($"Withdrew ${amount}. New balance: ${Balance}");
        }
        else
        {
            Console.WriteLine("Invalid withdrawal amount!");
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        BankAccount account = new BankAccount("Alex", 100.00);
        account.Deposit(50.00);
        account.Withdraw(25.00);
        Console.WriteLine($"{account.Owner} now has ${account.Balance}");
    }
}
```
- **Why it matters**: Properties can validate and clean data automatically
- **Git command**: `git add . && git commit -m "Add validation to Owner property"`

### 7. Build Complete Banking System 🏛️
- **What to do**: Replace your `Program.cs` with the version below. `Main` now creates a `BankAccount[]` array (one with an empty owner to test the validation), runs deposits and withdrawals (some invalid), and prints final balances.
- **File(s) touched**: Program.cs
- **Code snippet** (full file):
```csharp
namespace CSharp_Lesson_Six;

class BankAccount
{
    private string _owner;
    private double _balance;

    public string Owner
    {
        get { return _owner; }
        set
        {
            if (string.IsNullOrWhiteSpace(value))
            {
                Console.WriteLine("Owner name cannot be empty!");
                _owner = "Unknown Owner";
            }
            else
            {
                _owner = value.Trim();
            }
        }
    }

    public double Balance
    {
        get { return _balance; }
        private set { _balance = value; }
    }

    public BankAccount(string owner, double startingBalance)
    {
        Owner = owner;
        _balance = startingBalance >= 0 ? startingBalance : 0;
        Console.WriteLine($"Account created for {Owner} with ${Balance}");
    }

    public void Deposit(double amount)
    {
        if (amount > 0)
        {
            Balance += amount;
            Console.WriteLine($"Deposited ${amount}. New balance: ${Balance}");
        }
        else
        {
            Console.WriteLine("Deposit amount must be positive!");
        }
    }

    public void Withdraw(double amount)
    {
        if (amount > 0 && amount <= Balance)
        {
            Balance -= amount;
            Console.WriteLine($"Withdrew ${amount}. New balance: ${Balance}");
        }
        else
        {
            Console.WriteLine("Invalid withdrawal amount!");
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("=== Simple Banking System ===");

        BankAccount[] accounts = {
            new BankAccount("Alice", 500.00),
            new BankAccount("Bob", 250.00),
            new BankAccount("", 100.00)  // Test validation
        };

        Console.WriteLine("\n=== Account Activity ===");

        accounts[0].Deposit(50.00);
        accounts[0].Withdraw(25.00);
        accounts[0].Withdraw(1000.00);  // Should fail

        accounts[1].Deposit(-10.00);    // Should fail
        accounts[1].Withdraw(100.00);

        Console.WriteLine("\n=== Final Balances ===");
        foreach (var account in accounts)
        {
            Console.WriteLine($"{account.Owner}: ${account.Balance}");
        }
    }
}
```
- **Why it matters**: Properties and methods work together in real systems
- **Git command**: `git add . && git commit -m "Create complete banking system demo"`

### 8. Add Account Summary Method 📊
- **What to do**: Replace your `Program.cs` with the version below. `BankAccount` gains two more methods — `ShowAccountSummary()` prints a formatted block, and `CanAfford()` reports whether a withdrawal would be allowed. `Main` calls them at the end.
- **File(s) touched**: Program.cs
- **Code snippet** (full file):
```csharp
namespace CSharp_Lesson_Six;

class BankAccount
{
    private string _owner;
    private double _balance;

    public string Owner
    {
        get { return _owner; }
        set
        {
            if (string.IsNullOrWhiteSpace(value))
            {
                Console.WriteLine("Owner name cannot be empty!");
                _owner = "Unknown Owner";
            }
            else
            {
                _owner = value.Trim();
            }
        }
    }

    public double Balance
    {
        get { return _balance; }
        private set { _balance = value; }
    }

    public BankAccount(string owner, double startingBalance)
    {
        Owner = owner;
        _balance = startingBalance >= 0 ? startingBalance : 0;
        Console.WriteLine($"Account created for {Owner} with ${Balance}");
    }

    public void Deposit(double amount)
    {
        if (amount > 0)
        {
            Balance += amount;
            Console.WriteLine($"Deposited ${amount}. New balance: ${Balance}");
        }
        else
        {
            Console.WriteLine("Deposit amount must be positive!");
        }
    }

    public void Withdraw(double amount)
    {
        if (amount > 0 && amount <= Balance)
        {
            Balance -= amount;
            Console.WriteLine($"Withdrew ${amount}. New balance: ${Balance}");
        }
        else
        {
            Console.WriteLine("Invalid withdrawal amount!");
        }
    }

    public void ShowAccountSummary()
    {
        Console.WriteLine("==================");
        Console.WriteLine($"Account Owner: {Owner}");
        Console.WriteLine($"Current Balance: ${Balance:F2}");
        Console.WriteLine($"Account Status: {(Balance > 100 ? "Good Standing" : "Low Balance")}");
        Console.WriteLine("==================");
    }

    public bool CanAfford(double amount)
    {
        return amount > 0 && amount <= Balance;
    }
}

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("=== Simple Banking System ===");

        BankAccount[] accounts = {
            new BankAccount("Alice", 500.00),
            new BankAccount("Bob", 250.00),
            new BankAccount("", 100.00)  // Test validation
        };

        Console.WriteLine("\n=== Account Activity ===");

        accounts[0].Deposit(50.00);
        accounts[0].Withdraw(25.00);
        accounts[0].Withdraw(1000.00);  // Should fail

        accounts[1].Deposit(-10.00);    // Should fail
        accounts[1].Withdraw(100.00);

        Console.WriteLine("\n=== Account Summaries ===");
        foreach (var account in accounts)
        {
            account.ShowAccountSummary();
        }

        Console.WriteLine($"\nCan Alice afford a $400 withdrawal? {accounts[0].CanAfford(400.00)}");
    }
}
```
- **Why it matters**: Methods can format and analyze data
- **Git command**: `git add . && git commit -m "Add account summary and affordability check methods"`

### 9. Push Your Protected Code 🚀
- **What to do**: In GitHub Desktop → Commit changes → Push origin
- **File(s) touched**: Uploading to GitHub
- **Code snippet**: None
- **Why it matters**: Share your secure, well-designed classes
- **Git command**: `git push origin main`

## Run & Test ▶️
- Press Ctrl+F5 or click green ▶️ button in Rider
- **Expected output** after Step 8: three "Account created" messages (with the empty-owner one printing the validation warning and becoming "Unknown Owner"), a list of account activity (some succeeding, the $1000 withdrawal and $-10 deposit both failing), an account-summary block per account, and a "Can Alice afford a $400 withdrawal? True" line.

### Common errors and fixes
- **"Type 'Program' already defines a member called 'Main'"** — You have two `Main` methods. Make sure you replaced the whole file at each step instead of pasting on top of the old code. There should be exactly one `static void Main(string[] args)` in `Program.cs`.
- **"The entry point of the program is global code; ignoring 'Main(string[])' entry point"** — Same root cause: there's a stray line of code outside any method (often a leftover `Console.WriteLine("Hello, World!");` from the starter). Delete anything outside the `class BankAccount { ... }` and `class Program { ... }` braces.
- **"The property or indexer 'BankAccount.Balance' cannot be used in this context because the set accessor is inaccessible"** — You tried to set `Balance` from outside the `BankAccount` class (for example from inside `Main`). After Step 5 the setter is `private` — only `BankAccount`'s own methods can change `Balance`. Use `Deposit` or `Withdraw` instead.
- **"Cannot access private field"** — You tried to read or write `_balance` from outside `BankAccount`. Use the public `Balance` property instead.

## Bonus Challenge 🔥
Create a `Student` class with grade validation!

**Hint**:
```csharp
class Student
{
    private double _gpa;

    public string Name { get; set; }

    public double GPA
    {
        get { return _gpa; }
        set { _gpa = value >= 0.0 && value <= 4.0 ? value : 0.0; }
    }

    public void AddGrade(double points, int credits)
    {
        // Calculate new GPA logic here
        Console.WriteLine($"{Name}'s new GPA: {GPA:F2}");
    }

    public string GetGradeLevel()
    {
        return GPA >= 3.5 ? "Honor Roll" : "Regular";
    }
}
```
