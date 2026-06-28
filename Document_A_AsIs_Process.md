# Document A: As-Is Process Description

**Nordic Secure Bank - Customer Onboarding**

---

We received a request from Nordic Secure Bank (a fictitious bank) to redesign and improve their customer onboarding processes. At present, the process operates as described below and was originally designed and configured by a consulting company.

## The Normal Scenario

The bank has only one branch in central Stockholm, where Anna works as a clerk. She registers scanned customer requests by filling out a form in the system, which takes an average of 20 minutes per case. After registration, Kim, the credit investigator, checks the customer's credit using a website called UC, which takes around 25 minutes. He then records the result in the system, taking an additional 10 minutes. If the credit check result is not OK (which occurs in about 10% of cases) Elin, the CRM officer, writes and sends a rejection letter through the system, which notifies the customer by email. This task takes around 25 minutes.

If the credit check result is OK, the process continues. Elin enables the customer to update their profile, and Linda, an accounting assistant, enables incoming transactions. These two tasks are performed in parallel through the system, and each takes about 10 minutes. Once both tasks are completed, Elin informs the customer that they can use the system by sending a separate email, which takes 25 minutes. After this, a fraud investigator reviews the case for potential fraud. This is a very time-consuming step, as each case must be checked against several anti-money laundering rules. The bank currently employs two fraud investigators, Peter and Maria. The review takes around 3 hours.

In 80% of cases, no potential fraud is found. In these cases, Linda enables the customer to have full access, taking around 10 minutes, and Elin informs the customer by email, taking around 10 minutes. The process then ends.

If the fraud investigator identifies the case as a potential fraud case, they submit a request for external fraud investigation through a website. Filling in all required information takes around 30 minutes. In 90% of these cases, the bank receives the external investigation result within 1 day. If no result is received within 2 days, the fraud investigator sends a reminder through the external website, which takes around 10 minutes. This reminder step may repeat until a result is received.

Once the result arrives, the fraud investigator registers it in the internal system, which takes around 20 minutes. If the result indicates no fraud (about 90% of cases) Linda enables the customer to have full access, and Elin informs the customer as described earlier. If the result indicates fraud, Elin disables the customer's ability to update their profile, and Linda disables incoming transactions for the customer's account. These two tasks can be done in parallel and each takes around 10 minutes. Afterward, Elin sends a rejection letter by email, taking around 25 minutes, and the fraud investigator reports the case to the police, taking around 25 minutes. These two tasks can also be done in parallel. However, they cannot be performed in parallel with the earlier disabling tasks, because regulations require that the customer must not be able to take any action at the moment they are informed or reported to the police.

The bank recently hired another CRM officer, Paul, who can assist Elin. The reported time for each task includes a 5-minute setup time.
