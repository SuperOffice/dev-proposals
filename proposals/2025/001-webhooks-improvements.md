# Proposal: Webhooks Improvements

- **Author(s):** @superoffice-dx-team  
- **Status:** Draft  
- **Version:** 1.0  
- **Created:** 2025-09-17  
- **Updated:** 2025-09-17  

---

## 📖 Summary

Enhance the existing **webhooks system** in the SuperOffice REST API to provide more reliability, flexibility, and ease of use for partners and customers.  

---

## 🎯 Motivation

Webhooks are widely used by partners to integrate SuperOffice events into their own systems. Current limitations include:  

- Lack of **delivery guarantees** → missed events if the target endpoint is temporarily unavailable.  
- Limited **event filtering** → currently too broad, requiring clients to handle unnecessary payloads.  
- No **management APIs** → setup and maintenance of webhook subscriptions is manual and inflexible.  

Improving webhooks will reduce partner complexity, increase reliability, and align with modern API best practices.  

---

## 🛠️ Detailed Design

### 1. Delivery Reliability

- Provide a long-lived **dead-letter queue** for undeliverable events.

### 2. Event Filtering

- Allow webhook subscriptions to specify **entity types and event types** (e.g., `contact.created`, `appointment.updated`).  
- Support **payload shaping** (full entity vs. minimal delta).  

### 3. Management APIs

- Expose endpoints to:
  - `POST /webhooks` → create subscription  
  - `GET /webhooks` → list subscriptions  
  - `DELETE /webhooks/{id}` → remove subscription  
  - `PATCH /webhooks/{id}` → update subscription  

### 4. Monitoring

- Provide **delivery status logs** via API.  
- Optionally support **partner callback for health checks**.  

---

## 🔄 Alternatives Considered

- **Polling APIs** → rejected due to inefficiency.  
- **Event streaming (Kafka/WebSockets)** → considered, but too heavy for immediate adoption. Might complement webhooks in the future.  

---

## ❓ Open Questions

- Should retry limits be **configurable per subscription**, or fixed globally?  
- Should we allow **wildcard event types** (e.g., `contact.*`)?  
- How should **payload versioning** be handled (e.g., evolving schemas)?  

---

## 📅 Timeline (Draft)

- **Q4 2025** → Internal prototype & feedback loop with pilot partners.  
- **Q1 2026** → Public beta with documentation.  
- **Q2 2026** → General availability.  

---

## ✅ Status

Currently in **Draft** stage — open for partner and community feedback.  
Next steps: refine design, address open questions, and prepare for implementation.