import java.util.*;

// Account class to manage a single account
class Account {
    private String accountHolderName;
    private int accountNumber;
    private double balance;
    private List<String> transactionHistory;

    // Constructor
    public Account(String name, int accNum) {
        this.accountHolderName = name;
        this.accountNumber = accNum;
        this.balance = 0.0;
        this.transactionHistory = new ArrayList<>();
        transactionHistory.add("Account created with balance ₹0.0");
    }

    // Deposit money
    public void deposit(double amount) {
        if (amount <= 0) {
            System.out.println("❌ Deposit amount must be positive.");
            return;
        }
        balance += amount;
        transactionHistory.add("Deposited ₹" + amount + " | Balance: ₹" + balance);
        System.out.println("✅ ₹" + amount + " deposited successfully.");
    }

    // Withdraw money
    public void withdraw(double amount) {
        if (amount <= 0) {
            System.out.println("❌ Withdrawal amount must be positive.");
        } else if (amount > balance) {
            System.out.println("❌ Insufficient balance!");
        } else {
            balance -= amount;
            transactionHistory.add("Withdrew ₹" + amount + " | Balance: ₹" + balance);
            System.out.println("✅ ₹" + amount + " withdrawn successfully.");
        }
    }

    // Check balance
    public void checkBalance() {
        System.out.println("💰 Current Balance: ₹" + balance);
    }

    // Print transaction history
    public void printTransactionHistory() {
        System.out.println("📜 Transaction History:");
        for (String transaction : transactionHistory) {
            System.out.println(transaction);
        }
    }

    // Getters (optional, not used in this example)
    public int getAccountNumber() {
        return accountNumber;
    }

    public String getAccountHolderName() {
        return accountHolderName;
    }
}

// Main application class
public class SimpleBankingApp {
    private static final Scanner sc = new Scanner(System.in);
    private static Account account;

    public static void main(String[] args) {
        System.out.println("====== Welcome to Simple Bank ======");
        System.out.print("Enter Account Holder Name: ");
        String name = sc.nextLine();
        System.out.print("Enter Account Number: ");
        int accNum = sc.nextInt();

        account = new Account(name, accNum);

        int choice;
        do {
            System.out.println("\n==== Menu ====");
            System.out.println("1. Deposit");
            System.out.println("2. Withdraw");
            System.out.println("3. Check Balance");
            System.out.println("4. Transaction History");
            System.out.println("5. Exit");
            System.out.print("Enter your choice (1-5): ");
            choice = sc.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter amount to deposit: ₹");
                    double depAmount = sc.nextDouble();
                    account.deposit(depAmount);
                    break;
                case 2:
                    System.out.print("Enter amount to withdraw: ₹");
                    double withAmount = sc.nextDouble();
                    account.withdraw(withAmount);
                    break;
                case 3:
                    account.checkBalance();
                    break;
                case 4:
                    account.printTransactionHistory();
                    break;
                case 5:
                    System.out.println("🙏 Thank you for banking with us!");
                    break;
                default:
                    System.out.println("❌ Invalid choice. Please try again.");
            }

        } while (choice != 5);
    }
}
