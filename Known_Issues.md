# Known Issues & Handling

Observations from automating UIBank (a demo banking app) with UiPath. These are application-side behaviors found during development, along with how the workflows handle them.

## 1. Account frequently does not appear on the dashboard

| | |
|---|---|
| **Flows affected** | `Flow\Dashboard.xaml` (account list) and `Flow\Account.xaml` (opens account details). Account creation happens in `Flow\Apply New Account.xaml`. |
| **Symptom** | After an account is created, it often does not appear on the dashboard. Because `Account.xaml` opens the account from the dashboard, it cannot reach the account details when the account is missing. |
| **Reproducibility** | Frequent but inconsistent: the same steps sometimes show the account and sometimes do not. |
| **Likely cause** | Application-side inconsistency (delayed or inconsistent data in the demo app), not a selector or timing issue in the workflow. *(To confirm: check the create-account request/response in browser DevTools > Network.)* |
| **Impact** | Downstream flows (account details, transfer) cannot rely on the account being listed in the UI. |

### How the workflow handles it

- **Capture confirmation data at creation time.** The account number / success message is stored in a variable right after submit, so later flows do not depend on the dashboard list alone.
- **Retry with polling.** The flow reloads the dashboard and re-checks for the account up to N attempts, with a short wait between attempts (Retry Scope / Do While with a counter).
- **Fail clearly.** If the account is still missing after the last attempt, the flow throws a `BusinessRuleException` ("Account not found on dashboard") and logs the details.

## 2. (Add more here)

Add each new issue using the same format: flows affected, symptom, reproducibility, likely cause, impact, and handling. Only list behaviors you have actually reproduced.

---

*Note: UIBank is a demo application intended for practice, so inconsistent behavior is expected. These notes document how the automation stays reliable despite it.*
