# class-project
#python project on budget management
class CollegeBudgetManager:
    def __init__(self):
        self.budget = 0.0
        self.expenses = []  # List of dictionaries to store expenses

    def set_budget(self):
        try:
            amount = float(input("Enter your total monthly budget (e.g., allowance/earnings): "))
            if amount < 0:
                print("Budget cannot be negative.")
                return
            self.budget = amount
            print(f"Success! Monthly budget set to ${self.budget:.2f}\n")
        except ValueError:
            print("Please enter a valid number.\n")

    def add_expense(self):
        if self.budget == 0:
            print("Please set your monthly budget first!\n")
            return
        
        category = input("Enter category (e.g., Food, Rent, Books, Entertainment): ").strip()
        try:
            amount = float(input("Enter expense amount ($): "))
            if amount < 0:
                print("Expense amount cannot be negative.\n")
                return
            
            # Store expense as a dictionary
            expense = {"category": category.capitalize(), "amount": amount}
            self.expenses.append(expense)
            print(f"Added ${amount:.2f} under '{category.capitalize()}'.\n")
        except ValueError:
            print("Please enter a valid amount.\n")

    def view_summary(self):
        total_spent = sum(item["amount"] for item in self.expenses)
        remaining = self.budget - total_spent

        print("\n--- Monthly Financial Summary ---")
        print(f"Total Budget  : ${self.budget:.2f}")
        print(f"Total Spent   : ${total_spent:.2f}")
        print(f"Remaining     : ${remaining:.2f}")

        # Budget alert for college students
        if remaining < 0:
            print("⚠️ Alert: You have exceeded your budget! Time to cut back.")
        elif remaining < (self.budget * 0.2):
            print("⚠️ Warning: You are running low on funds (less than 20% left).")
        else:
            print("✅ You are doing great! Budget is under control.")
        print("---------------------------------\n")

    def view_category_breakdown(self):
        if not self.expenses:
            print("No expenses recorded yet.\n")
            return

        # Aggregate spending by category
        breakdown = {}
        for item in self.expenses:
            cat = item["category"]
            breakdown[cat] = breakdown.get(cat, 0.0) + item["amount"]

        print("\n--- Category-wise Spending ---")
        for cat, amt in breakdown.items():
            print(f"{cat}: ${amt:.2f}")
        print("------------------------------\n")

def main():
    manager = CollegeBudgetManager()
    
    while True:
        print("=== College Student Budget Manager ===")
        print("1. Set Monthly Budget")
        print("2. Add Expense")
        print("3. View Overall Summary & Alerts")
        print("4. View Category Breakdown")
        print("5. Exit")
        
        choice = input("Choose an option (1-5): ").strip()
        
        if choice == '1':
            manager.set_budget()
        elif choice == '2':
            manager.add_expense()
        elif choice == '3':
            manager.view_summary()
        elif choice == '4':
            manager.view_category_breakdown()
        elif choice == '5':
            print("Exiting Budget Manager. Good luck with your studies!")
            break
        else:
            print("Invalid choice! Please select between 1 and 5.\n")

if __name__ == "__main__":
    main()
