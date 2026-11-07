# AIquainted analytics event contract (v1.0.0)

No analytics provider or tracker is connected in the local MVP. `assets/site.js` provides a provider-neutral event queue (`window.aiquaintedEvents`) and dispatches `aiquainted:event`. Production integration must map this contract without collecting prompt contents, card data, or unnecessary personal data.

| Event | Trigger | Required properties | Notes |
|---|---|---|---|
| `visit` | One per page load | `page_path`, `occurred_at`, `contract_version` | Referrer optional |
| `lead_submit` | Valid lead accepted by service | `offer`, provider lead ID | Current preview emits `configured:false`; no data stored |
| `lead_delivery` | Resource delivered/confirmed | `offer`, provider lead ID, delivery status | Server/provider evidence preferred |
| `checkout_start` | Checkout button opens provider checkout | `product`, `configured` | Current disabled control emits preview event only |
| `purchase` | Verified provider webhook | provider order ID, product, currency, gross amount | Never trust browser success page alone |
| `refund` | Verified provider webhook/admin record | provider order ID, amount, currency, reason category | Exclude free-text and payment data |

## Identity and privacy
Use pseudonymous session/lead/order identifiers. Do not place email, name, prompt text, or payment data into event properties. Consent requirements and retention must be decided before enabling a production adapter. Purchase/refund must be emitted from verified Lemon Squeezy webhook evidence, with idempotency by provider event/order ID.
