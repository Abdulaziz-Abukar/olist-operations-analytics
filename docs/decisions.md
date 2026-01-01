# Decisions

**Decision:** Use an order-item transactional fact as the primary fact table: `fact_order_items` at 1 row per order item

**Grain:** One row represents one purchased item line within an order (order_id + order_item_id + product_id + seller_id)

**Rationale:**

- Revenue and freight are recorded at order-item level
- Seller and product category slicing requires item-level grain to avoid allocations
- Supports seller performance, category mix, and geographic analysis without losing detail

**Tradeoffs:**

- Order-level metrics (delivery SLAs, cancellations, review rates) risk double-counting if computed directly from item grain
- **Mitigation**: create a complementary `fact_orders` table at 1 row per order for lifecycle and delivery metrics

**Outcome:**

- Core revenue analysis is performed on `fact_order_items`
- Delivery, cancellation, and review KPIs are performed on `fact_orders`
- Both facts share conformed dimensions (date, customer, seller, product/category, geography)
