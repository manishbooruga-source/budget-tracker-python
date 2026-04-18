#Budget Tracker
# This database helps users track their income and expenses.
# It allows users to add, view, and categorize their financial transactions.
class BudgetTracker:
    def __init__(self):
        self.transactions = []

    def add_transaction(self, amount, category, description=''):
        transaction = {
            'amount': amount,
            'category': category,
            'description': description
        }
        self.transactions.append(transaction)
        return "Transaction added successfully."

    def view_transactions(self):
        if not self.transactions:
            return "No transactions recorded."
        result = "Transactions:\n"
        for idx, transaction in enumerate(self.transactions, start=1):
            result += f"{idx}. Amount: {transaction['amount']}, Category: {transaction['category']}, Description: {transaction['description']}\n"
        return result

    def get_total_expenses(self):
        total = sum(t['amount'] for t in self.transactions if t['amount'] < 0)
        return f"Total Expenses: {total}"

    def get_total_income(self):
        total = sum(t['amount'] for t in self.transactions if t['amount'] > 0)
        return f"Total Income: {total}"
if __name__ == "__main__":
    tracker = BudgetTracker()
    while True:
        action = input("Would you like to (a)dd a transaction, (v)iew transactions, (t)otal income, (e)xpenses or (q)uit? ").lower()
        if action == 'a':
            amount = float(input("Enter amount (negative for expenses, positive for income): "))
            category = input("Enter category: ")
            description = input("Enter description (optional): ")
            print(tracker.add_transaction(amount, category, description))
        elif action == 'v':
            print(tracker.view_transactions())
        elif action == 't':
            print(tracker.get_total_income())
        elif action == 'e':
            print(tracker.get_total_expenses())
        elif action == 'q':
            print("Exiting Budget Tracker. Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")
