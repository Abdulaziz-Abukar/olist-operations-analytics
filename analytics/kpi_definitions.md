# KPI Definitiosn

## Orders & Revenue

**1. Total Orders**

- Purpose: Demand trend + growth/decline detection
- Formula: `count(distinct order_id)`
- Grain: order

**2. Total Revenue (GMV)**

- Purpose: Commercial peformance over time
- Formula: `sum(order_item_price + freight_value)`
- Grain: order item → aggregated to order/time

**3. Average Order Value (AOV)**

- Purpose: Monetization efficiency
- Formula: `Total Revenue / Total Orders`
- Grain: order (aggregated)

## Delivery & Logistics

**4. On-Time Delivery Rate**

- Purpose: SLA performance + customer trust
- Formula: `delivered_on_or_before_estimated / delivered_orders`
- Grain: delivered order

**5. Average Delivery Duration (days)**

- Purpose: Speed-to-customer baseline
- Formula: `avg(delivered_date - approved_date)`
- Grain: delivered order

**6. Late Delivery Rate**

- Purpose: Identify delay burden by seller/region
- Formula: `late_delivered_orders / delivered_orders`
- Grain: delivered order

## Seller Reliability

**7. Cancellation Rate**

- Purpose: Seller ops relaibility + leakage
- Formula: `canceled_orders / total_orders`
- Grain: order

**8. Seller On-Time Delivery Rate**

- Purpose: Rank sellers, find chronic offenders
- Formula: same as (4), sliced by seller
- Grain: delivered order

## Customer Experience Signals

**9. Average Review Score**

- Purpose: Satisfaction proxy
- Formula: `avg(review_score)`
- Grain: reviewed order

**10. Review Rate**

- Purpose: Bias detection + coverage
- Formula: `reviewed_orders / delivered_orders`
- Grain: order
