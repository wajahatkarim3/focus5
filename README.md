# Focus5

**Five tasks a day. One timer. One at a time.**

Live: **[focus.shipkaro.dev](https://focus.shipkaro.dev)**

Focus5 is a focus app for people whose to-do list has become the thing they are avoiding. It
refuses to hold everything. You pick five tasks for today, and it runs one timer against one of
them.

This repository is the public overview. The product source is private.

## What it does

| | |
| --- | --- |
| **Focus 5** | Five tasks, one timer, one at a time. |
| **Book Focus** | Run a session inside a single book. |
| **Brain Dump** | Talk, and get back sorted tasks. |
| **Insights** | Where your focus actually went. |
| **Library** | Books to hold the rest, so today stays five. |

Today, Agenda and Calendar are free. The focus timer, Brain Dump, Insights and unlimited books
are premium.

## Status

The web app is live and sells. The Android app is built and instrumented, and is not on Google
Play yet.

## Stack

**Android:** Kotlin, Jetpack Compose, Material 3, Koin, Room, DataStore, Retrofit, Navigation
Compose. Single module, package by feature. Built on [NowKit](https://kit.shipkaro.dev).

**Web:** Next.js 16, React 19, TypeScript, deployed on Vercel.

**Backend:** Supabase for auth, Postgres and Edge Functions. Row level security decides access,
so the client is never the authority on who paid.

**Billing:** RevenueCat on both clients, with Stripe Billing and Managed Payments behind the web
checkout. One `premium` entitlement, one webhook, both clients read the same server answer.

**Voice:** Deepgram Nova-3 streaming speech to text, with `google/gemini-2.5-flash` over
OpenRouter turning a ramble into structured tasks. Roughly one cent per brain dump.

**Analytics:** PostHog on both clients speaking one shared event vocabulary, plus GA4 on the
marketing page.

## Built with Stripe Projects

RevenueCat was provisioned through [Stripe Projects](https://docs.stripe.com/projects):

```bash
stripe projects add revenuecat/app
```

That created the RevenueCat app, connected Stripe as the payment gateway, and wrote the
credentials into the project environment. The `web` offering carries one product, the Founder
Pack, attached to the `premium` entitlement that the Android app already gated on. A purchase on
either client unlocks both, because RevenueCat's `app_user_id` is the same uuid as Supabase's
`auth.uid()`.

Stack: `RevenueCat / app`. Project `focus5`, on Stripe account RemoteKaro LLC.

## Pricing

One payment of $29 for the Founder Pack. Lifetime access, nothing to renew, no subscription to
cancel. That is a deliberate constraint, not a launch promotion, and the landing page is built
around it.

## Author

Built by [Wajahat Karim](https://wajahatkarim.com) at RemoteKaro LLC.

Submitted to RevenueCat Shipaton 2026.
