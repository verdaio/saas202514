# Lightweight Dunning Alerts

## Pricing

**Headline:** Recover failed payments fast.  
**Subhead:** Listen to Stripe failures, trigger smart retries and branded nudges, track recovered MRR.

### Plans
- **Solo — $19/mo**: up to $50k ARR, Stripe connect, email nudges, smart retry schedule, recovery dashboard.
- **Team — $39/mo**: up to $250k ARR, SMS, Slack alerts, custom windows, A/B message tests.
- **Growth — $79/mo**: up to $1M ARR, multi-project, webhook API, segment rules, custom domains.
- **Scale — custom**: >$1M ARR, IP allowlist, SSO, priority support.

**Add-ons:** $0.02 per SMS sent. Email included.  
**Guarantee:** If recovered MRR is zero after 30 days, you don’t pay.  
**CTA:** Connect Stripe. See recovered invoices this week.

---

## Data Schema (DDL)

```sql
CREATE TABLE merchant(id UUID PRIMARY KEY, name TEXT, plan TEXT, created_at TIMESTAMPTZ);
CREATE TABLE customer(id UUID PRIMARY KEY, merchant_id UUID, external_id TEXT, email TEXT, status TEXT, FOREIGN KEY (merchant_id) REFERENCES merchant(id));

CREATE TABLE subscription(id UUID PRIMARY KEY, merchant_id UUID, customer_id UUID, status TEXT, amount NUMERIC, currency TEXT, current_period_end TIMESTAMPTZ, FOREIGN KEY (merchant_id) REFERENCES merchant(id), FOREIGN KEY (customer_id) REFERENCES customer(id));
CREATE TABLE invoice(id UUID PRIMARY KEY, merchant_id UUID, external_id TEXT, customer_id UUID, due_at TIMESTAMPTZ, amount_due NUMERIC, status TEXT, FOREIGN KEY (merchant_id) REFERENCES merchant(id), FOREIGN KEY (customer_id) REFERENCES customer(id));
CREATE TABLE payment_attempt(id UUID PRIMARY KEY, merchant_id UUID, invoice_id UUID, failed_at TIMESTAMPTZ, failure_code TEXT, will_retry_at TIMESTAMPTZ, FOREIGN KEY (merchant_id) REFERENCES merchant(id), FOREIGN KEY (invoice_id) REFERENCES invoice(id));

CREATE TABLE workflow(id UUID PRIMARY KEY, merchant_id UUID, name TEXT, enabled BOOLEAN, FOREIGN KEY (merchant_id) REFERENCES merchant(id));
CREATE TABLE workflow_step(id UUID PRIMARY KEY, workflow_id UUID, kind TEXT, delay_hours INT, template_id UUID, FOREIGN KEY (workflow_id) REFERENCES workflow(id));
CREATE TABLE template(id UUID PRIMARY KEY, merchant_id UUID, channel TEXT, subject TEXT, body TEXT, FOREIGN KEY (merchant_id) REFERENCES merchant(id));

CREATE TABLE message(id UUID PRIMARY KEY, merchant_id UUID, invoice_id UUID, channel TEXT, sent_at TIMESTAMPTZ, status TEXT, FOREIGN KEY (merchant_id) REFERENCES merchant(id), FOREIGN KEY (invoice_id) REFERENCES invoice(id));
CREATE TABLE recovery_event(id UUID PRIMARY KEY, merchant_id UUID, invoice_id UUID, recovered_at TIMESTAMPTZ, amount NUMERIC, FOREIGN KEY (merchant_id) REFERENCES merchant(id), FOREIGN KEY (invoice_id) REFERENCES invoice(id));
```

---

## API Endpoints (REST)

- `POST /v1/stripe/authorize` connect account  
- `POST /v1/workflows` create workflow  
- `POST /v1/workflows/{id}/steps` add step `{kind: "email"|"sms"|"retry", delay_hours, template_id}`  
- `POST /v1/templates` create message template  
- `GET /v1/invoices?status=failed` list failed invoices  
- `POST /v1/invoices/{id}/retry` trigger retry  
- `POST /v1/invoices/{id}/paylink` create secure update-card link  
- `GET /v1/metrics/recovery?range=last_30d` recovered MRR, recovery rate, time-to-recover  
- `POST /v1/alerts/slack` configure webhook  
- **Webhooks:** `POST /v1/webhooks/stripe` receive `invoice.payment_failed|succeeded`, `customer.source.expiring`

---

## Cold Outreach (10)

1. What share of your churn is failed payments? We plug into Stripe and recover a chunk in days.  
2. Your team writes dunning emails every month. We automate them and show recovered MRR.  
3. Baseline Stripe retries are fine. We add targeted windows and better messages.  
4. You’ll get Slack alerts on high-value failures and a pay-link that updates the card in one click.  
5. If recovered MRR is zero in 30 days, you don’t pay. Low risk.  
6. Want to A/B your dunning copy without a dev? Toggle templates and measure uplift.  
7. International cards failing at odd hours? Shift retries to the customer’s local time.  
8. Stop spamming everyone. Segment by tenure and ARPA, then nudge differently.  
9. I can connect to your Stripe sandbox and show a full workflow in 15 minutes.  
10. Send me last month’s failed invoices count. I’ll project a conservative recovery.

---

## Notes

- Keep all endpoints JSON. Use idempotency keys on writes.  
- Encrypt tokens at rest. Log only event IDs.  
- Ship with audit trails and exportable data from day one.
