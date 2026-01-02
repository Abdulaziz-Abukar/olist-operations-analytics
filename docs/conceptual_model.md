# Conceptual Model (v1)

![Conceptual Model Diagram](/diagrams/Conceptual_Diagram.png)

This document defines the high-leel business entities and relationships for the Olist e-commerce analytics warehouse. The diagram above provides a visual overview; detailed explainations follow below.

## Entities

- Customer
- Order
- Order Item
- Product
- Seller
- Payment
- Shipment / Delivery
- Review
- Geography (Customer Location, Seller Location)
- Product Category

## Relationships

- Customer (1) → (M) Order
- Order (1) → (M) Order Item
- Product (1) → (M) Order Item
- Seller (1) → (M) Order Item
- Order (1) → (M) Payment
  - Note: Orders may have multiple payment records (installments)
- Order (1) → (1) Shipment / Delivery
  - Note: Delivery timestamps belong to the order lifecycle (purchase/approval/shipped/delivered)
- Order (1) → (0..1) Review
  - Note: Not all delivered orders are reviewed.
- Product Category (1) → (M) Product
- Geography (1) → (M) Customer
- Geography (1) → (M) Seller
  - Note: Customer and seller geographies may be modeled as separate role-playing relationships to the same Geography entity

## Key Constraints / Modeling Notes

- Revenue is item-level (Order Item), while delivery SLAs are order-level (Order)
- Order_level metrics must avoid double-counting when joined to Order Item.
- Reviews attach to Orders (not items) and should be optional
- Payments are multi-row per order and should not be used directly for revenue without business rules.
