# code-challenge-ledger

We'd like you to demonstrate your code-writing capability with a short exercise.

As we expect of all engineers, if you have any questions, please don't hesitate to ask. We've kept the question straightforward enough where this should not take too long, but in the worst case, make a decision and let us know what that decision was.

Email us or link us to your solution, which should consider the following:

- It does not include any personally identifiable information - we'd like to evaluate this blindly!
- It includes a README walking through your approach and any decisions made.
- It is done on your own schedule, in a single digit number of hours.
- The code is representative of a quality you would have in a real project, including tests.
- There is no need for saving results to a file, display on any web page, or anything else - command-line-only output is appropriate.

# Problem Statement

Your objective is to build a basic ledger for loans. We lend money to customers (principal), and interest accrues daily on this principal. As each payment comes in, the interest balance is paid off first, and then principal is paid off.

For example, if there is a 0.1% daily interest rate, and we loan money on day 0, here is an example of how balances are accrued and payments are applied:

| Day | Action   | Principal Bal | Interest Bal | Outstanding |
|-----|----------|--------------:|-------------:|------------:|
| 0   |          |        100.00 |         0.00 |      100.00 |
| 1   |          |        100.00 |         0.10 |      100.10 |
| 2   |          |        100.00 |         0.20 |      100.20 |
| 3   |          |        100.00 |         0.30 |      100.30 |
| 3   | Pay 0.15 |        100.00 |         0.15 |      100.15 |
| 4   |          |        100.00 |         0.25 |      100.25 |
| 3   | Pay 1.00 |         99.25 |         0.00 |       99.25 |


Your code should read in a CSV of a specific format, and calculate the daily balances based on the day after the last date in the CSV.

You can assume:
- the CSV is in chronological order
- the file is not corrupted and is well-formatted within the CSV specification
- loans will not be funded more than once
- max one payment per day per loan
- interest accrual rounds down to the nearest penny daily
- event chronology is interest accrual, loan funding, payment processing
- payments are applied after the interest is accrued

Fields:
`date,id,action,amount,apr`

- Date: In YYYY-MM-DD format.
- ID: Loan ID, positive integer
- Action: "fund_loan" is a loan being created with an initial principal balance; "payment" is an amount paid by the customer against its balance.
- Amount: The amount funded or the payment amount, both positive currency (float with max two decimal places)
- APR: only provided for "fund_loan" lines, float as %, showing the APR (not the daily accrual %)

Input format:
```
2023-01-01,1,fund_loan,5000.00,5.0
2023-01-06,2,fund_loan,6000.00,6.0
2023-02-10,1,payment,94.36,
2023-02-11,2,payment,116.00,
2023-03-10,1,payment,94.36,
2023-03-11,2,payment,116.00,
```

Output should denote all balances on the calendar day after the last input entry in the format, after daily interest accrual. (Stated differently, this would be the payoff amount if paid that day.) If a loan is paid off, it would be expected that principal and interest balances would be 0, but should still be reported.

Fields:
`date,id,principal,interest,total`

- Date: In YYYY-MM-DD format, the day after the last input date.
- ID: Integer, one line per loan ID in the input file, in numerical order.
- Principal: Principal balance.
- Interest: Interest balance.
- Total: Principal + Interest

Expected output:
```
2023-03-12,1,4857.24,1.32,4858.56
2023-03-12,2,5835.34,0.95,5836.29
```

A larger and more complex example is included in the repository.

# Evaluation Criteria

Above isn't doing the most cutting-edge engineering - instead, we're focusing on the most reliable, well-understood, and highly-trusted software.

We definitely don't want you spending too much time on this code snippet, but we would like it to reflect how you think about solving problems on a small scale. Document the design decisions you made, or other on-the-ground choices you made as you implemented the solution. Your code should be consistent in its style, both in readability and design choices. Ensure your code has appropriate test coverage, testing a couple common use cases. Break things apart to be readable, but there isn't a need for an over-abstraction.
