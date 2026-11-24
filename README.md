# OOAD-PART-B

This Maven project is a worked implementation of the five Part B stages:
1. Core model classes
2. JavaFX boundary/view classes
3. Controllers
4. SQLite JDBC database and DAO classes
5. Integration checks and testing guidance

## Technology
- Java 17
- JavaFX 21
- Maven
- SQLite JDBC
- JUnit 5

## Open in GitHub Codespaces
1. Create/open your GitHub repository.
2. Upload/extract this project so `pom.xml` is at the repository root.
3. Open Terminal in Codespaces.
4. Confirm Java and Maven:
   ```bash
   java -version
   mvn -version
   ```
5. Compile and run tests:
   ```bash
   mvn test
   ```
6. Run the JavaFX application:
   ```bash
   mvn javafx:run
   ```

The first run creates `banking.db` in the project working directory.

## Application workflow
- Register a customer.
- Log in using the registered username and password.
- Open a Savings, Investment or Cheque Account.
- View accounts, deposit, withdraw where allowed, apply monthly interest, and view transactions.
- Log out.

## Account rules from Part A
- Savings: monthly interest 0.05%; withdrawals are prohibited.
- Investment: monthly interest 5%; minimum opening deposit BWP500.
- Cheque: available only to employed customers; employer name and address required.
- Cheque account interest is not calculated because Part A does not specify a rate.

## Architecture
- `model`: domain classes and banking rules.
- `view`: JavaFX screens; collect/display user input only.
- `controller`: validates input and coordinates model/DAO operations.
- `dao`: JDBC CRUD operations.
- `database`: SQLite connection and schema initialization.
- `security`: PBKDF2 password hashing and verification.

## Important notes before assessment
- This is an educational assignment implementation, not production banking software.
- Account balance updates and transaction inserts are grouped in one JDBC transaction in `AccountDAO.updateBalanceAndRecordTransaction`, so both are committed together or rolled back together.
- DAO CRUD coverage is intentionally basic and can be expanded with additional update/delete screens if your lecturer expects every CRUD operation exposed through the GUI.
- The provided JUnit tests cover core rules and password hashing. The README manual integration test below should also be completed and its actual results recorded.
- Test the project in your own Codespace and do not claim tests passed until you have run them.

## Manual end-to-end integration test record
Run these tests in the JavaFX application and record the actual result/date:
1. Register an employed customer using a unique username and password of at least 8 characters.
2. Log in using the same credentials; confirm the dashboard opens.
3. Open a Savings Account with BWP1,000.
4. Try withdrawing BWP100 from Savings; confirm the application rejects it.
5. Deposit BWP200 into Savings; confirm the balance is BWP1,200.
6. Apply monthly Savings interest; expected interest is BWP0.60 and new balance BWP1,200.60.
7. Open an Investment Account with BWP1,000; attempt BWP100 withdrawal; expected balance after withdrawal is BWP900.
8. Apply monthly interest to the BWP900 Investment balance; expected interest is BWP45 and new balance BWP945.
9. Try opening an Investment Account with BWP499; confirm rejection.
10. Open a Cheque Account for an employed customer and enter employer details; confirm success.
11. View transaction history and confirm successful operations appear.
12. Log out and confirm the login screen returns.

## Git commands
```bash
git status
git add .
git commit -m "Implement Part B banking system"
git push origin main
```
