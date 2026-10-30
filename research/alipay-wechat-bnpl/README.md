# How Alipay/Huabei and WeChat/Fenfu handle fraud and AML risk

[Đọc toàn bộ bằng tiếng Việt](vi/README.md)

Research date: **31 October 2026**. Geography: **mainland China**. This report concerns public evidence about purchase-related consumer credit and adjacent credit features; it is not an internal-system audit or a comprehensive legal opinion.

## Main findings

1. **Separate the wallet from the lender.** Alipay and WeChat Pay are payment interfaces/ecosystems. The actual loan can involve a consumer-finance company, microlender or bank partner. The loan agreement determines the responsible lender. Do not assume one universal lender or that WeBank supplies all WeChat-associated credit.
2. **There is no single “fraud/AML score” established by these sources.** Identity/authentication, credit assessment, transaction/merchant restrictions, ongoing monitoring and AML investigation/reporting are different functions. They can share information without sharing the same objective or decision.
3. **The product definitions have evolved.** Current Huabei disclosure includes authorized cash-type consumer loans. The June 2026 Fenfu manual describes gradually available transfers and a bank-borrowing test, alongside consumption credit. These are not equivalent to fabricated purchases used to circumvent product restrictions.
4. **Public evidence supports layered controls, not a verified internal model architecture.** Contracts/manuals disclose checks, data-processing purposes and possible interventions. Group AI/AML statements do not establish which model runs in a particular BNPL product, how often it fails, or whether every listed data field is used in each decision.
5. **AML reporting is a separate accountable process.** Applicable reporting rules require human analysis and documented disposition of monitoring alerts. Automated alert generation or report preparation does not establish autonomous filing decisions.

## 1. What products and entities are being compared?

| Ecosystem | Product boundary | Entity boundary and evidence |
|---|---|---|
| Alipay / Ant | Huabei (花呗): revolving consumer credit, purchase/instalment features, and separately described cash-type credit in the July 2026 disclosure | Ant Consumer Finance publishes the current product disclosure. The publicly reachable Huabei contract distinguishes credit providers from Alipay's payment role, but has undated/legacy provider language. It is not a current exhaustive lender roster. [A-S1, A-S2] |
| WeChat | Fenfu (分付): daily-interest consumer credit by default, selected merchant instalment offers and additional features depending on eligibility | One public contract names JinCheng Consumer Finance as lender, Tenpay as payment operator and Weiheng as technology/service adviser. Another dated DBS disclosure describes a different co-lending arrangement. Neither describes every customer's loan. [W1–W3] |

**Do not equate Fenfu with WeChat Pay Score or Weilidai.** Pay Score is a separate merchant-service product; its August 2026 agreement restricts use for financing/credit services. The Fenfu manual distinguishes it from Weilidai. A score used to offer deposit waivers is not automatically a documented underwriting input for a consumer loan. [W1, W4, W9]

Primary product sources: [Ant Consumer Finance disclosure](https://www.myxiaojin.cn/notice/detail/6), [Fenfu manual](https://pay.weixin.qq.com/doc/user/4021837995), [DBS collaboration disclosure](https://www.dbs.com.cn/iwov-resources/doc/footer/Payment_Installment_Service_Description.pdf). Exact contract applicability and feature availability should be checked against the customer's current account agreement.

## 2. Side-by-side control comparison

Labels: **PRODUCT** = named-product document; **PLATFORM** = broader payment ecosystem; **GROUP** = corporate statement; **REQUIREMENT** = regulatory obligation, not proof of implementation. An undated contract establishes what it says, not that it is the operative agreement for all customers today.

| Control stage | Alipay / Huabei evidence | WeChat / Fenfu evidence | What can be concluded |
|---|---|---|---|
| Identity and onboarding | Published Huabei contract requires truthful information and identity verification. **PRODUCT; version uncertainty** [A-S2] | Manual requires real-name identity, a mainland bank card and normal payment-account status. Identity-document renewal is explicitly connected to AML obligations. **PRODUCT** [W1] | Both disclose identity controls. Only Fenfu's fetched current manual provides this particularly direct ongoing-AML link. This does not prove relative effectiveness. |
| Account misuse / authentication | Huabei contract covers credential protection and impersonation reporting. Exact current BNPL biometric/device implementation was not verified. [A-S2] | Tenpay privacy policy describes risk-sensitive authentication and additional verification for account recovery. **PLATFORM**, not a universal Fenfu authentication flow [W5] | Authentication helps address account misuse. Public evidence is insufficient to compare account-takeover detection rates. |
| Credit approval and limits | Risk assessment and changing credit limits in published contract. [A-S2] | Eligibility, limits, interest and repayment/credit-record provisions in manual and partner contracts. [W1–W3] | These primarily address credit risk; a limit reduction is not automatically an AML decision. |
| Transaction legitimacy and permitted purpose | Published contract prohibits fabricated orders/sham cash-out, permits security-related suspension, and uses transaction/refund/dispute information. **PRODUCT; version uncertainty** [A-S2] | Real-time system assessment in manual; partner contract prohibits fake-order activity and unlawful cash-out, and permits temporary restrictions. **PRODUCT / partner-specific** [W1, W2] | Both disclose controls against misuse of consumer credit. Exact model inputs and thresholds remain unknown. |
| Merchant controls | Merchant contract provides identity/business verification, risk-information exchange, limits, suspension and delayed settlement. **PLATFORM; undated** [A-S3] | Merchant agreement covers merchant checks, activity inconsistent with the business profile, settlement delays and restrictions. **PLATFORM; current version unverified** [W6] | Merchant/acquiring controls complement borrower-side controls. These clauses do not prove every action applies identically to each BNPL transaction. |
| Ongoing financial-crime monitoring | Ant describes group indicator governance and AML/report automation. **GROUP self-report** [A-S4] | Fenfu partner contract permits relevant identity, transaction, fund-flow and device/network data for AML/anti-scam purposes; Tencent policy describes monitoring/reporting. **PRODUCT permission + GROUP policy** [W2, W7] | There is evidence of monitoring purposes and governance. Data permission is not a model specification or evidence of detection performance. |
| Review and reporting | Public evidence does not reconstruct Huabei's case-review or filing approval workflow. | Public evidence does not reconstruct Fenfu's investigator workflow or filing approval chain. | Applicable rules require human alert analysis and reasons for reporting/exclusion. **REQUIREMENT** [R3]. Do not turn this obligation into an observed provider implementation. |
| Data governance | Merchant contract has credential/security/confidentiality provisions; a complete current Huabei privacy inventory was not verified. [A-S3] | Tenpay policy covers risk-related processing, security and legally required retention. **PLATFORM** [W5] | Interface deletion is not proof of backend erasure. Legal recordkeeping and privacy must be considered together. |

## 3. How to interpret the lifecycle

This is an **analytical model assembled from disclosed controls**, not a leaked or reconstructed production architecture.

1. **Identify the customer and responsible entities.** Distinguish the payment account from the lending relationship and applicable product terms.
2. **Authenticate and assess access.** Identity and account-integrity controls address impersonation and account misuse; credit eligibility addresses borrowing eligibility.
3. **Assess the proposed transaction.** Product purpose, transaction legitimacy and merchant context can affect permission to proceed. A genuine identity does not guarantee a genuine transaction.
4. **Apply a proportionate action.** A payment may be declined, further evidence requested, service restricted or settlement delayed where the applicable terms/law support it. These actions are not synonymous with a regulatory asset freeze.
5. **Continue monitoring after checkout.** Refunds, disputes, repayment and fund-flow records may matter to different risk functions. Refund accounting itself must not be presented as a proven AML algorithm.
6. **Review suspicious activity separately.** AML monitoring leads to documented analysis and, where warranted, a report by the responsible institution. Keep the evidence trail and decision distinct from a customer-service or credit decision.
7. **Maintain records and update diligence.** Applicable rules require ongoing review and retention; statutory obligations do not establish the quality of an individual provider's implementation. [R1–R3]

### Four examples that prevent category errors

- **Unauthorized account use:** an identity/authentication fraud concern, even if the loan is repaid.
- **Fabricated merchant purchase:** prohibited-use/fraud concern; additional evidence determines whether there is also an AML issue.
- **Authorized transfer or cash-loan feature:** not inherently fraudulent or money laundering. Verify the particular product's permitted use.
- **A genuine borrower who cannot repay:** primarily credit/default risk. Delinquency alone does not prove fraud or laundering.

See [risk taxonomy](RISK-TAXONOMY.md) for the distinctions between fraud, credit, AML, operational and data-governance risks.

## 4. What is actually known about AI and detection technology?

**Ant:** a July 2025 company-issued announcement describes unified AML indicators, RiskKey/iGuardian and automation, mentioning AI-related capabilities. This is a corporate self-report across a wider business scope. It does not establish that Huabei uses each named component or that an LLM makes independent filing decisions. A June 2026 Xinhua article reports Ant Consumer Finance's scene-specific real-time risk assessment, but the underlying original sustainability report was not retrieved; treat the description as secondary coverage of company claims. [A-S4, A-S5]

**Tencent:** its AML policy and 2024 ESG report describe risk-based governance, higher-risk diligence, reporting, testing/training and the use of big data/machine learning. These support a group-level account, not a Fenfu-specific claim about graph neural networks, LLM agents, social-chat-content processing, model weights or detection accuracy. [W7, W8]

**Conclusion:** public documentation supports combinations of policy, identity checks, risk assessment, monitoring and review. It does not support a precise “here is their fraud algorithm” comparison. More detailed public data permissions on one side should not be mistaken for evidence that side has stronger controls.

## 5. Regulatory context and operating-effectiveness limits

The revised AML law took effect in January 2025. The CDD measures effective January 2026 explicitly cover consumer-finance companies and nonbank payments, with relevant provisions applying to online microlenders. The reporting amendments effective December 2025 explicitly require human analysis and documented reasons for reporting or excluding monitoring alerts. These sources establish obligations, not a provider audit. [R1–R3]

The rules verified for this research specify at least ten-year retention for relevant identity/transaction records, with scope and timing defined in the rules; do not reuse older generic five-year summaries. Customer-risk measures must also respect applicable proportionality and asset-freeze boundaries. For the full citations, timing and qualifications, see [regulatory findings](regulatory-findings.md).

Historical enforcement is evidence that impressive technology claims do not establish perfect controls. The 2023 Ant aggregate penalty covered multiple categories and was not a Huabei-specific or AML-only fine. Tencent's Tenpay disclosure concerned past payment-service breaches and management's rectification statement; it was not a Fenfu-specific finding. This research does not infer current product effectiveness from either penalty or a company's claim of remediation. [R4, R5]

## 6. What remains unknown

Public evidence reviewed does **not** establish:

- Current production rule thresholds, model feature weights or shared architecture between products.
- BNPL-specific fraud loss, false-positive/negative rates or AML detection accuracy.
- Exact alert-routing queues, investigator staffing, case SLA or filing volumes.
- A current complete lender roster and operative agreement for every customer.
- Huabei's complete current privacy/retention inventory or the original Ant Consumer Finance sustainability report behind the secondary coverage.
- Whether any named AI capability is deployed in the exact product/version used by a particular borrower.

Best next evidence, if access becomes available: the relevant in-app lending contract and privacy notice; the current lender's product documentation; regulator or independently assured control disclosures; and original technical reports with deployment scope. Do not request customer credentials or real sensitive transaction records just to fill these gaps.

## 7. Evidence files and method

TinyFish searches and fetches covered three workstreams. **19 distinct source documents were substantively inspected**: five for Ant/Huabei, nine for WeChat/Fenfu, and five for regulatory context. Long-report sections were reviewed where relevant; this count does not mean every page of every report was read. Eighteen sources are official/issuer documents or official reproductions, and one is secondary news coverage. Failed retrievals and search-only leads are excluded from that count.

- [Alipay/Huabei findings and five-source register](alipay-findings.md)
- [WeChat/Fenfu findings and nine-source register](wechat-findings.md)
- [Regulatory findings and five-source register](regulatory-findings.md)
- [Scope and evidence rules](RESEARCH-SCOPE.md)
- [Risk taxonomy](RISK-TAXONOMY.md)

Citation key: A-S1–A-S5 correspond to S1–S5 in the Alipay report; W1–W9 and R1–R5 correspond to the WeChat and regulatory registers. Each register records dates, scope and retrieval limitations. Product manuals and contracts are evidence of disclosed behavior/rights, not independent certification of operating effectiveness.
