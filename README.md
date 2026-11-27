# UIPath Portfolio Testing UIBank

A UIPath RPA project that automates banking flows on UIBank, a demo banking web app. The main deliverable is an end-to-end transfer flow, built from smaller reusable workflows (login, dashboard navigation, account details, transfer)

## Workflows

**End-to-end flow**

| Workflow | File | Description |
|---|---|---|
| E2E Transfer | `Transfer\E2E Transfer.xaml` | Full transfer scenario from start to finish. This is the entry point to run. |

**Reusable building blocks** (`Flow\`)

| Workflow | File | Description |
|---|---|---|
| Login | `Flow\Login.xaml` | Logs in to UIBank. |
| Dashboard | `Flow\Dashboard.xaml` | Navigates the dashboard. |
| Apply New Account | `Flow\Apply New Account.xaml` | Applies for / creates a new account. |
| Account | `Flow\Account.xaml` | Account-related actions. |
| Apply Loan | `Flow\Apply Loan.xaml` | Starts a loan application. |
| Input Loan | `Flow\Input Loan.xaml` | Fills in the loan details. |

> `Main.xaml` is not used in this project. Run `Transfer\E2E Transfer.xaml` directly.

## Tech Stack

- UiPath Studio (low-code XAML workflows)
- UiPath.UIAutomation, Excel, Mail, System, and Testing activities

## Getting Started

1. Clone this repository.
2. Open `project.json` in UiPath Studio.
3. Restore dependencies when prompted.
4. Fill in the required inputs in `Data` before running. *(TODO: describe your config/test data file and which values are needed)*
5. Set `Transfer\E2E Transfer.xaml` as the file to run (or run it directly).

> Use a demo UIBank account only. Do not commit real credentials.

## Known Issues

UIBank is a demo app and behaves inconsistently at times. For example, a newly created account sometimes does not appear in the account list. See [KNOWN_ISSUES.md](https://github.com/syolandita/Portfolio_Automation-Using-UIPath/blob/main/Known_Issues.md) for the full list and how the workflows handle each case (retry/polling, capturing confirmation data, and clear exceptions).

## Project Structure

```
Flow/        Reusable workflows (Login, Dashboard, Account, Loan, ...)
Transfer/    End-to-end transfer workflow
Data/        Config and input data
Test Data/   Test data for test cases
```
