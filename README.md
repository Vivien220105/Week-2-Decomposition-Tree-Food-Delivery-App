# Week-2-Decomposition-Tree-Food-Delivery-App
[README.md](https://github.com/user-attachments/files/32453440/README.md)
Food Delivery Platform — System Decomposition

Revision 2 — from order placement to delivery confirmation.

A top-down decomposition of a food delivery platform connecting customers, restaurants, and drivers. Every subsystem is tagged with the decomposition type used to split it into its children, and every leaf component is scoped to a single, atomic responsibility.

10 subsystems · 39 atomic components · 4 decomposition types

Contents
Decomposition types
Root
1. Customer Ordering
2. Restaurant Catalog Management
3. Restaurant Order Handling
4. Driver Dispatch & Delivery Execution
5. Payments & Financials
6. Notifications & Communication
7. Account & Identity Management
8. Ratings, Feedback & Trust
9. Order Lifecycle & State
10. Platform Operations, Risk & Reporting
Open questions for the room
Decomposition types
Type	Split by
Functional	what each part does
Process	ordered steps in a workflow
Object	the real-world actor/entity each part concerns
Data	the category of information each part owns
Root — Food Delivery Platform System

Connects customers, restaurants, and drivers across the full order lifecycle — from browsing a menu to a confirmed hand-off at the door.

Split → Level 1: functional — ten subsystems, grouped mostly by the distinct capability each one performs. One of the ten, Order Lifecycle & State, is object-shaped rather than functional (see open questions).

1. Customer Ordering — process

Discovery, cart, checkout, and tracking happen in a fixed order within one order, so the split follows the process.

1.1 Discovery & Search — Browse restaurants and menus; filter by cuisine, price, ETA.
1.2 Cart Management — Add, remove, and modify items before checkout.
1.3 Checkout & Order Placement — Capture address, tip, and instructions; submit the order.
1.4 Order Tracking (Customer View) — Live map/ETA view, subscribed to the order's status feed.
2. Restaurant Catalog Management — data

Menu, pricing, and stock are three categories of catalog data edited on their own schedule, so the split is by data.

2.1 Menu & Item Listings — Create and organize items and categories.
2.2 Item Pricing & Modifiers — Set prices and optional add-ons per item.
2.3 Stock & Inventory Flags — Mark items in or out of stock in real time.
3. Restaurant Order Handling — process

Being open, accepting, and preparing form a fixed per-order sequence, so the split is by process.

3.1 Restaurant Availability Control — Toggle open/closed; throttle intake in busy-mode.
3.2 Order Acceptance / Rejection — Confirm or decline within a service window.
3.3 Kitchen Preparation Tracking — Mark prep stages; signal "ready for pickup."
4. Driver Dispatch & Delivery Execution — process

Availability, matching, navigation, pickup, and confirmation happen in a fixed order for one delivery, so the split is by process.

4.1 Availability & Location Tracking — Driver on/offline state and live GPS position.
4.2 Order–Driver Matching — Assign the nearest eligible driver to a ready order.
4.3 Route Navigation & ETA — Turn-by-turn guidance and arrival estimates.
4.4 Pickup Confirmation — Driver confirms receipt at the restaurant.
4.5 Delivery Confirmation — Photo, PIN, or signature at the customer's door.
5. Payments & Financials — functional

Calculating, charging, paying out, refunding, and configuring rates are distinct operations with no fixed order, so the split is functional.

5.1 Fare & Price Calculation — Item total, delivery fee, tax, and tip.
5.2 Payment Processing — Charge and authorize the customer's payment method.
5.3 Driver & Restaurant Payouts — Settle earnings on schedule.
5.4 Refunds & Disputes — Reverse or adjust charges on cancellations/complaints.
5.5 Pricing & Promotions Config — Commission, delivery-fee, and discount rules.
6. Notifications & Communication — object

Each child is scoped to one recipient — customer, restaurant, or driver — so the split follows the object being messaged.

6.1 Customer Notifications — Status, ETA changes, and promo alerts.
6.2 Restaurant Notifications — New order and cancellation alerts.
6.3 Driver Notifications — New assignment and route-update alerts.
6.4 Chat & Support Messaging — Direct messaging between parties and support.
7. Account & Identity Management — data

Each child owns one category of stored data — credentials, profile, roles, sessions — so the split is by data.

7.1 Registration & Authentication — Sign-up, login, credential verification.
7.2 Profile & Address Management — Personal details, saved addresses, payment methods.
7.3 Role & Permission Management — Customer, restaurant, and driver access levels.
7.4 Session & Device Management — Active sessions, tokens, registered devices.
8. Ratings, Feedback & Trust — object

Each child is scoped to who or what is being rated, so the split follows the object under review.

8.1 Restaurant Ratings & Reviews — Customer feedback on food and restaurant.
8.2 Driver Ratings — Customer feedback on the delivery experience.
8.3 Customer Ratings — Restaurant/driver feedback on customer conduct.
8.4 Complaint & Issue Reporting — Intake for disputes ratings don't cover.
9. Order Lifecycle & State — object

Each child manages one facet of the same object — the order itself — so the split is object-based.

9.1 Order State Machine — Valid statuses and legal transitions between them.
9.2 Order History & Audit Log — Full timeline for receipts, support, disputes.
9.3 Cancellation Handling — Who can cancel when, and the resulting side effects.
9.4 Status Change Propagation — Publishes transitions to tracking, notifications, apps.
10. Platform Operations, Risk & Reporting — functional

Fraud detection, ticketing, and reporting are distinct capabilities, though grouped mainly by being internal-facing.

10.1 Fraud & Abuse Detection — Flag suspicious orders, accounts, or payments.
10.2 Support Ticketing & Escalation — Internal handling of issues raised by 8.4.
10.3 Business Intelligence & Reporting — Metrics for growth, ops, and finance.
Open questions for the room
Branches 2 & 3 — Should Catalog Management and Order Handling be two subsystems, or one branch with two leaves?
Branch 9 — Does Order Lifecycle & State deserve root-level peer status, or is it shared infrastructure the other branches should just reference?
Branch 10 — Fraud detection, ticketing, and reporting share no real function, actor, or data — genuine subsystem, or leftover catch-all?

Every leaf above is atomic — one clear responsibility, no further split needed to stand as one implementable service or module.
