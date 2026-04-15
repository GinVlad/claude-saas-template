# Payments Rules

## Provider
- Recommended: Stripe (most SaaS-friendly)
- Alternatives: Paddle, LemonSqueezy

## Integration Points
1. Checkout (subscription creation)
2. Webhooks (payment events)
3. Customer Portal (manage subscription)

## Flow
```
User clicks "Upgrade"
    → Create Checkout Session (server)
    → Redirect to hosted checkout
    → User pays
    → Provider sends webhook
    → Server updates subscription
    → User redirected to success page
```

## Webhook Events to Handle
- `checkout.session.completed` — New subscription
- `invoice.paid` — Recurring payment success
- `customer.subscription.updated` — Plan change
- `customer.subscription.deleted` — Cancellation

## Webhook Security
- Always verify webhook signature
- Use webhook secret from environment
- Return 200 quickly, process async if needed

## Idempotency
- Store processed webhook event IDs
- Check before processing to avoid duplicates

## Test Mode
- Use test keys for development
- Never use live keys in development
- Test all webhook scenarios
