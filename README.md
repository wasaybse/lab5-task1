Design a simple program of concurrency by implementing the scenario of two account holders in a joint bank account. (Hint: Total amount will be 50000, if ‘user A’ wants to withdraw 45,000 and ‘user B’ wants to withdraw 20,000) Apply mechanism of synchronization e.g. Block or Method for handling accessibility of multi-threads:

    package wasay1;
    class BankAccount {
    private int balance = 50000;
    synchronized void withdraw(String user, int amount) {
        System.out.println(user + " is trying to withdraw " + amount);
        if (balance >= amount) {
            System.out.println(user + " is proceeding...");
            balance -= amount;
            System.out.println(user + " successfully withdrew " + amount);
        } else {
            System.out.println("Insufficient balance for " + user);
        }
        System.out.println("Remaining balance: " + balance + "\n");
    }
    }
    class WithdrawThread extends Thread {
    BankAccount acc;
    String user;
    int amount;
    WithdrawThread(BankAccount acc, String user, int amount) {
        this.acc = acc;
        this.user = user;
        this.amount = amount;
    }
    public void run() {
        acc.withdraw(user, amount);
    }
    }
    public class Wasay1 {
    public static void main(String[] args) {

        BankAccount account = new BankAccount();

        WithdrawThread t1 = new WithdrawThread(account, "wasay", 45000);
        WithdrawThread t2 = new WithdrawThread(account, "001", 20000);

        t1.start();
        t2.start();
    }
}
