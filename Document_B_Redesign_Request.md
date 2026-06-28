# Document B: Redesign Request

**Nordic Secure Bank - Customer Onboarding Automation**

---

The company finds out that the business cannot scale with the current process set up, so they aim to go through heavy automation. They will serve customers like before, but they also enable customer to register by sending email to specific email of the company and an AI-agent will extract the information and register them. In addition, we aim to enable customer to register themselves via an online form. We expect 20% of customers to register themselves via an online form, 20% register like before and 60% can be registered via AI-Agents.

From the total number of customers that AI Agents aim to register, we expect that the system may fail to complete approximately 20% of them. In such instances, the registration will be handed over to a clerk for manual processing.

Also, we intend to automate sending credit check requests to UC and receiving results back through the web service provided by UC in a synchronous way. Also, we will inform customers through email - except for rejection letters that will be sent manually due to their importance to the company. Also, all of these functionalities can be automated by calling web services asynchronously: like enabling and disabling customer profiles web service, enabling and disabling incoming transactions web service, and enabling and disabling full access webservice. Note that each of these functions are separate webservices. Also, we will switch and automate any request that will be made for external fraud investigation. This automation will not change the time that we receive the result for the external investigator but can remove manual work to initiate the request. Also, we aim to automate reporting cases to police through a web service provided by police.

Reviewing the potential fraud is tricky. The company will invest in developing an AI agent that identifies potential fraud cases automatically by comparing them with the bank's regulations. The data scientist team told us that the model would have very low false negatives but could have some false positives due to imbalanced data. This means that we can rely on the result if the model predicts that there is no fraud. However, we cannot be sure that the case is a potential fraud if the model predicts so. Based on the early investigation, they said 80% of cases would be classified as "no fraud". For the rest, we will keep our manual fraud review to avoid paying a lot to external services.
