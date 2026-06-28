# Breakeven Analysis – *fund‑comply*

---

## 1. Cost per Active User (USD / month)

| Component | Assumptions | Cost per active user |
|-----------|-------------|----------------------|
| **Compute** (AWS Lambda / Fargate, 1 GB‑hour) | 0.1 GB‑hour * 0.0000167 USD = **$0.00167** | **$0.10** |
| **Storage** (S3, 10 GB per user) | 10 GB * 0.023 USD/GB = **$0.23** | **$0.05** |
| **Bandwidth** (Outbound, 1 GB per user) | 1 GB * 0.09 USD/GB = **$0.09** | **$0.02** |
| **Support & Misc** (monitoring, ops) | Flat $200/month / 1,000 users | **$0.20** |
| **Total** | | **$0.17** |

> **Key take‑away** – operating cost per active user is **$0.17/mo**, leaving a very high gross margin once subscription revenue is added.

---

## 2. Pricing Tiers

| Tier | Monthly Price | Core Features |
|------|---------------|---------------|
| **Basic** | **$10** | • Compliance template library<br>• Basic regulatory reporting<br>• Email support |
| **Standard** | **$25** | • All Basic features<br>• Advanced reporting & analytics<br>• Audit‑log export<br>• 24/7 chat support |
| **Premium** | **$50** | • All Standard features<br>• Full automation (auto‑submission to regulators)<br>• Custom dashboards<br>• Dedicated account manager |

> **Margin** – Gross margin ≈ 80 % (costs are only 20 % of revenue).

---

## 3. CAC (Customer Acquisition Cost)

| Channel | Avg. CAC |
|---------|----------|
| Digital ads + content | $200 |
| Partner referral | $250 |
| In‑person demos | $300 |

**Range** – **$200 – $300** per new paying user.

---

## 4. LTV (Lifetime Value)

Assumptions: 12‑month average contract, 80 % gross margin, churn 0 % (idealized).

| Tier | Monthly Rev | Annual Rev | Gross Profit | LTV |
|------|-------------|------------|--------------|-----|
| Basic | $10 | $120 | $96 | **$96** |
| Standard | $25 | $300 | $240 | **$240** |
| Premium | $50 | $600 | $480 | **$480** |

> **Pay‑back**  
> CAC $250 / LTV $240 ≈ 1.04 months for Standard;  
> CAC $250 / LTV $96 ≈ 2.6 months for Basic;  
> CAC $250 / LTV $480 ≈ 0.52 months for Premium.

---

## 5. Break‑Even Users Count

Fixed operating cost (hosting, dev ops, sales & marketing) ≈ **$5,000 / month**.

| Tier | Gross Profit per User | Break‑Even Users |
|------|-----------------------|------------------|
| Basic | $8 | 625 |
| Standard | $20 | 250 |
| Premium | $40 | 125 |

> **Interpretation** – Once we acquire 250 Standard users (or 125 Premium users), the product covers all fixed costs and starts generating profit.

---

## 6. Path to $10 k MRR

| Tier | Users Needed | MRR |
|------|--------------|-----|
| Basic | 1,000 | $10,000 |
| Standard | 400 | $10,000 |
| Premium | 200 | $10,000 |

> **Strategic recommendation** – Target **400 Standard users** for the first 3‑month runway; this is the sweet spot between acquisition cost, churn risk, and revenue density.

---

### Bottom‑Line

* **Cost per active user**: $0.17/mo → **$0.83** annual.  
* **Gross margin**: 80 % → **$8–$40** profit per user/month.  
* **Break‑even**: 125 Premium users (or 250 Standard).  
* **$10 k MRR** achievable with 200 Premium users or 400 Standard users.  
* **CAC vs. LTV**: Pay‑back < 3 months across all tiers; Premium delivers the fastest ROI.

These figures give us a clear runway and a concrete target for the next funding round.