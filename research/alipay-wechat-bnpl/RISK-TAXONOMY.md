# Keep the risk categories separate

This is an analytical framework for interpreting the provider evidence, not a claim about either provider's internal organization or models.

| Category | Question being answered | Examples of evidence to inspect | Important limit |
|---|---|---|---|
| Identity / account fraud | Is this the legitimate customer, acting with valid authority? | Identity checks, authentication, account-change and device-risk handling | A genuine customer can still be deceived by a scam |
| Transaction / merchant fraud | Is the underlying transaction genuine and permitted? | Merchant/product restrictions, sham-transaction provisions, disputed payment handling | An anomaly or a contract violation does not alone establish a crime |
| Credit risk | Is the borrower eligible and likely able to repay? | Credit assessment, affordability/limit decisions, repayment performance | Default is not automatically fraud or money laundering |
| AML / counter-terrorist financing | Does the relationship or flow raise concerns requiring due diligence, analysis or reporting? | Customer identification, ongoing monitoring, documented review and reports by the obligated institution | A suspicious report is not a criminal conviction; a transaction decline is not proof a report was filed |
| Operational / model risk | Can the controls function reliably and proportionately? | Human escalation, error handling, appeal/correction and records | Public descriptions usually do not establish operating effectiveness |
| Data governance | Is data collected, shared and retained for a defined lawful purpose? | Product privacy notices, permissions, entity boundaries and legal retention rules | A privacy notice does not reveal model weights or prove every datum is used for every decision |

## Product boundary

Treat purchase-linked deferred payment/instalments separately from revolving consumer credit, authorized transfers and authorized cash consumer loans. An expanded product feature can be legitimate while a fabricated purchase used to bypass restrictions remains prohibited. Do not carry an old “cannot transfer / cannot cash out” summary into a current product without checking current product terms.

## Evidence boundary

Maintain separate columns for (1) product contract/manual, (2) ecosystem-wide disclosures, (3) legal requirements, (4) historical technical papers, and (5) inference. Similar vocabulary is not proof that two products use the same implementation.
