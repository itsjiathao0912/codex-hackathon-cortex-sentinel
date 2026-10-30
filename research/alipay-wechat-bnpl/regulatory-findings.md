# Mainland China AML context for Huabei and Fenfu research

Research date: 2026-10-31. Scope: public rules and historical enforcement context for mainland-China lending/payment institutions. These sources establish obligations and historical events, **not evidence that a particular Huabei/Fenfu control is implemented, effective, or identical across entities**. This is research context, not a comprehensive legal compliance opinion.

## Verified evidence register

| ID | Source / date | Supported finding and scope | Evidence strength |
|---|---|---|---|
| R1 | [PRC Anti-Money Laundering Law, 2024 revision](http://lawdb.cncourt.org/show.php?fid=157968), adopted 2024-11-08; effective 2025-01-01 | National-law text reproduced by China Court's law database, source attributed there to Xinhua. Articles 6/63 cover financial institutions including nonbank payment institutions. Articles 28–30 establish identity checks and ongoing risk-based diligence. Articles 34–35 establish retention and reports. Articles 40–41 establish list-based special preventive measures. | High for reproduced legal text; not an implementation audit |
| R2 | [Customer Due Diligence and Customer Identity/Transaction Record Retention Measures](https://www.moj.gov.cn/pub/sfbgw/flfggz/flfggzbmgz/202512/t20251224_529734.html), official Ministry of Justice reproduction; effective 2026-01-01 under Article 52 | Covers consumer-finance companies and nonbank payment institutions (Article 2); online microlenders are covered by relevant provisions (Article 47). Customer onboarding, merchant-acquiring diligence, ongoing review, enhanced due diligence, records and confidentiality are specified. | High for official rule text |
| R3 | [PBOC decision amending/repealing rules](https://www.moj.gov.cn/pub/sfbgw/flfggz/flfggzbmgz/202512/t20251230_529967.html), page states publication 2025-09-30; effective 2025-12-01 | Amendments to reporting and supervisory rules explicitly cover nonbank payments/consumer finance and relevant online microlenders; require human analysis of transaction-monitoring alerts, documented disposition, customer-centered monitoring and accountable governance. | High for official amendment text; URL date differs from displayed publication date |
| R4 | [Financial regulators' platform-rectification announcement](https://www.csrc.gov.cn/csrc/c100028/c7418599/content.shtml), CSRC, 2023-07-07 | Ant Group and subsidiaries faced a combined RMB7.123 billion penalty/confiscation covering several historical violation categories, including AML obligations. Announcement also identifies Tenpay among other penalized entities. | High for historical regulator statement; not Huabei/Fenfu-specific |
| R5 | [Tencent voluntary announcement](https://static.www.tencent.com/uploads/2023/08/17/f195adb5f3a9ee6cbe997bc28555ae1e.pdf), document signed 2023-07-07 | Tencent disclosed approximately RMB2.99 billion penalty on Tenpay for past mainland payment-service breaches; says PBOC inspected in 2021 and that Tenpay completed self-inspection and corresponding rectification. | Primary issuer disclosure; rectification effectiveness remains a company claim |

## What the framework requires, without assuming implementation

**R1: risk-based obligations and rights.** The law requires CDD and ongoing monitoring, not just a one-off identity check. Higher-risk relationships may require information on sources/uses of funds. Relevant identity records are retained at least ten years after the relationship ends, transaction information at least ten years after transaction completion. Suspicious reports are confidential. Institutions must obtain relevant official lists and check customers/counterparties. Measures must be proportionate; customers can challenge risk-management decisions. Reliance on third-party CDD does not remove the institution's legal responsibility. These are statutory obligations, not proof that either BNPL product uses any particular model or screening vendor. [R1]

**R2: onboarding, merchants, refresh, and data.** Articles 16–19 distinguish payment-account/customer diligence, merchant-acquiring diligence, and consumer-finance relationship onboarding. Articles 25–30 call for risk classification, ongoing review and additional investigation when behavior does not fit the known customer. Higher-risk cases can require additional information, intensified monitoring and senior approval. Article 28 says risk restrictions must not become unlawful asset freezes. Articles 43–44 require secure, confidential, reconstructable records and at least ten-year retention, with longer preservation for ongoing AML investigations where applicable. Article 51 provides transition periods for existing customers, so legal effective date alone is not evidence every old account was immediately refreshed. [R2]

**R3: an alert is not a filed suspicious-transaction report.** The amended reporting rule requires **human analysis and identification** of transactions selected by monitoring standards. Both reporting and non-reporting decisions need documented reasons; additional CDD can inform disposition and risk-rating changes. Monitoring is customer-centered and must cover customers and business lines. Governance includes accountable personnel, internal controls, training, audit and necessary systems. Relevant report and analysis records must be retained for at least ten years. This supports a distinction between automated detection and a reviewed AML disposition; it does not expose either provider's internal thresholds, staffing, case system or filing volumes. [R3]

## Operational interpretation for this research

The following is a synthesis of the rules, **not a reconstructed provider architecture**:

1. Identify which legal entity opens the account, provides payment/acquiring services, and lends the money.
2. Verify identity and, for applicable organizational customers, ownership/control; understand intended activity.
3. Classify risk and check relevant official lists.
4. Monitor customer/merchant activity and refresh diligence when evidence changes.
5. Review alerts, collect context, document why a case is excluded or reported.
6. Submit required reports through the responsible obligated institution; apply lawful, proportionate risk measures separately.
7. Retain auditable records securely and support review, complaints and regulatory investigation.

**Important distinctions:** A credit decline is not an AML finding. A suspicious-transaction report is not a criminal conviction. An automated fraud block is not necessarily a regulatory asset freeze. Authorized cash borrowing or an authorized transfer feature is not inherently deceptive cash-out or money laundering. Product-permitted behavior, fictitious-trade abuse, proceeds of crime and ordinary repayment difficulties require different evidence and responses.

## What enforcement proves—and does not prove

The 2023 Ant announcement establishes historical failings across several business/control categories; the RMB7.123 billion aggregate is **not an AML-only fine** and cannot be assigned to Huabei. It states that most prominent platform financial-business issues had undergone rectification and supervision was shifting to normalized regulation. This does not certify every current product control. [R4]

Tencent's filing confirms the Tenpay penalty and management's rectification statement, but does not itemize all AML failings in its own text. The referenced historical PBOC detailed notice failed retrieval with `page_not_found`; do not present its specific findings as directly verified here. Nor should a payment-company penalty be treated as a Fenfu-product penalty. [R5]

## Retrieval and limits

- Five substantive documents read in full: R1–R5, all Chinese except R5 English.
- NFRA's law page returned a JavaScript template rather than substantive text; the law was verified using R1 instead.
- Historical PBOC Tenpay notice linked in R5 could not be retrieved. No claim relies on its unseen details.
- Search-result snippets were used only to locate sources. Searches included legal status/effective dates, CDD/reporting rules, Ant/Tenpay historical enforcement.
- No claim of a comprehensive search for every later amendment, product contract, or legal entity relationship. Provider-specific terms must establish the entity and permitted use for the actual product/version being discussed.
- No confidential detection thresholds, reporting volumes, feature weights or current effectiveness statistics are established by these sources.
