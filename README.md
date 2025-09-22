# Personal Expense Tracker for 12 Months with Monthly Savings

# Initial Setup
monthly_income = 6000
monthly_savings = 1000
categories = ["Groceries", "Rent", "Utilities", "Car", "Health", "Phone"]

# Fixed Monthly Expenses (Total = $2,867)
fixed_expenses = [
    {"description": "Groceries", "amount": 100, "category": "Groceries"},
    {"description": "Rent", "amount": 1500, "category": "Rent"},
    {"description": "Utilities", "amount": 500, "category": "Utilities"},
    {"description": "Car Note + Insurance", "amount": 400, "category": "Car"},
    {"description": "Health Insurance", "amount": 117, "category": "Health"},
    {"description": "Phone Bill", "amount": 250, "category": "Phone"},
]

# Confirm total of fixed expenses
fixed_total = sum(item["amount"] for item in fixed_expenses)
print(f"Fixed monthly expenses total: ${fixed_total:.2f}")  # Should be $2,867.00

# Track total savings
total_savings = 0

# Loop for 12 months
for month in range(1, 13):
    print(f"\n--- Month {month} ---")

    # Start with fixed expenses each month
    monthly_expenses = fixed_expenses.copy()

    # Optional: Ask user to add any extra expenses
    add_more = input("Do you want to add any extra expenses this month? (yes/no): ").lower()
    if add_more == "yes":
        while True:
            desc = input("Enter description: ")
            try:
                amount = float(input("Enter amount: "))
            except ValueError:
                print("Invalid amount. Skipping this entry.")
                continue
            print("Categories:", ", ".join(categories))
            category = input("Enter category: ")
            monthly_expenses.append({"description": desc, "amount": amount, "category": category})

            more = input("Add another expense? (yes/no): ").lower()
            if more != "yes":
                break

    # Calculate total expenses
    total_expenses = sum(exp["amount"] for exp in monthly_expenses)
    remaining_balance = monthly_income - total_expenses

    # Add savings if possible
    if remaining_balance >= monthly_savings:
        saved = monthly_savings
        remaining_balance -= saved
    else:
        saved = max(0, remaining_balance)
        remaining_balance = 0

    total_savings += saved

    # Display monthly summary
    print("\n--- Monthly Summary ---")
    print(f"Total Expenses: ${total_expenses:.2f}")
    print(f"Savings Added: ${saved:.2f}")
    print(f"Remaining Balance: ${remaining_balance:.2f}")
    print(f"Total Savings So Far: ${total_savings:.2f}")

# Final summary
print("\n=== Yearly Summary ===")
print(f"Total Savings After 12 Months: ${total_savings:.2f}")
