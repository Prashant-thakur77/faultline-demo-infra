# faultline-demo-infra

The infrastructure repo of the synthetic system that [Faultline](https://github.com/Prashant-thakur77/Faultline) watches in its live demo. Nothing here runs in production; the data is synthetic.

- `flags.json`: the feature flags of the demo shop (an OpenTelemetry-Demo-shaped system). `paymentGate` is the containment lever: when it is off, checkout accepts orders and defers the charge, so payment failures stop failing checkout.
- `deploys.json`: deploys pinned or rolled back by Faultline.

Faultline changes this repo only through one human-approved action: it opens a pull request from a `faultline/fix-*` branch whose body carries the approved plan hash and an idempotency key, merges it after approval, and then verifies the change at `main` through a second channel before it records the result (APPLIED, NOT_APPLIED or UNKNOWN). Every pull request here was made that way.
