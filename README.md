# 🎯 C# Properties & Methods Project

## Lesson Snapshot
Build a smart bank account system that protects money and tracks transactions automatically! (Ages 8-18)

## Folder & File Map
```
PropertiesAndMethods/
├── .git/
├── .gitignore
├── PropertiesAndMethods.csproj
└── Program.cs
```

## Step-by-Step Build Guide

### 1. Fork and Clone the Repository ✅
- **What to do**: Go to [https://github.com/PhillyCoderDojo/CSharp-Lesson-6](https://github.com/PhillyCoderDojo/CSharp-Lesson-6) → Click "Fork" → Open GitHub Desktop → Clone your fork
- **File(s) touched**: Creating project folder
- **Code snippet**: None
- **Why it matters**: Get your workspace for advanced class features
- **Git command**: `git clone https://github.com/YOUR-USERNAME/CSharp-Lesson-6.git`

### 2. Open Project in Rider ✅
- **What to do**: Open Rider → File → Open → Select your cloned folder → Click OK
- **File(s) touched**: Loading project
- **Code snippet**: None
- **Why it matters**: Time to master properties and methods!
- **Git command**: None

### 3. Create Basic Account Class 🏦
- **What to do**: Open Program.cs and create a simple bank account
- **File(s) touched**: Program.cs
- **Code snippet**:
```csharp
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
- **What to do**: Give the account deposit and withdraw abilities
- **File(s) touched**: Program.cs (add to BankAccount class)
- **Code snippet**:
```csharp
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
```
- **Why it matters**: Methods control how data changes
- **Git command**: `git add . && git commit -m "Add Deposit and Withdraw methods"`

### 5. Convert Fields to Properties 🔒
- **What to do**: Protect the balance with a property instead of public field
- **File(s) touched**: Program.cs (update BankAccount class)
- **Code snippet**:
```csharp
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
    
    // Keep your Deposit and Withdraw methods here
}
```
- **Why it matters**: Properties control who can read/write data
- **Git command**: `git add . && git commit -m "Convert balance to protected property"`

### 6. Add Advanced Property Validation 🛡️
- **What to do**: Make the Owner property smarter about names
- **File(s) touched**: Program.cs (update Owner property)
- **Code snippet**:
```csharp
private string _owner;

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
```
- **Why it matters**: Properties can validate and clean data automatically
- **Git command**: `git add . && git commit -m "Add validation to Owner property"`

### 7. Build Complete Banking System 🏛️
- **What to do**: Create a full banking program with multiple accounts
- **File(s) touched**: Program.cs (update Main method)
- **Code snippet**:
```csharp
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
```
- **Why it matters**: Properties and methods work together in real systems
- **Git command**: `git add . && git commit -m "Create complete banking system demo"`

### 8. Add Account Summary Method 📊
- **What to do**: Create a method that shows formatted account information
- **File(s) touched**: Program.cs (add to BankAccount class)
- **Code snippet**:
```csharp
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
- **Expected output**: Account creation, successful/failed transactions, validation messages, final balances
- **Common error**: "Cannot access private field" - trying to access _balance directly
- **Fix**: Use the Balance property instead of _balance field

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
