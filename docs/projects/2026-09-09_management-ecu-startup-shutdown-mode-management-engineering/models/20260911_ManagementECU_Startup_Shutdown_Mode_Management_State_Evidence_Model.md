# Management ECU Startup / Shutdown / ECU Mode Management State Evidence Model

Date: 2026-09-11
Status: Sol-reviewed projection; upstream states never auto-prove downstream states

## States

- semantic authority exists
- product/configuration procedure exists
- project design accepted
- configured/generated artifact exists
- build/deployment result exists
- runtime observation exists
- requirement compared
- verdict assigned
- coverage assessed

## Separation rules

- Semantic authority existing does not prove a product/configuration procedure exists.
- A product/configuration procedure existing does not prove the Management ECU project design is accepted.
- An accepted project design does not prove a configured/generated artifact exists.
- A configured/generated artifact existing does not prove build/deployment success.
- Build/deployment success does not prove any runtime lifecycle behavior was observed.
- Configured initialization order never proves observed runtime startup order.
- Validation success never proves generation success, compile/link, deployment or runtime behavior.
- A StartOS transfer observation never proves runnable execution or application readiness.
- A RUN/POST_RUN request observation never proves RUN state or functional readiness.
- A mode-request observation never proves rule evaluation, Action List selection, action invocation or downstream outcome.
- A BswM action invocation never proves downstream service/job completion, EcuM implementation, NvM completion or durable persistence.
- A shutdown-request observation never proves target selection, late-shutdown execution or physical power loss.
- A wakeup-detection observation never proves wakeup validation or reaction.
- Any observation never proves a requirement verdict by itself.
- Any verdict never proves coverage by itself.

## Reading the matrix with this model

The public coverage matrix reports authority/configuration status separately from execution evidence status. `ECUM-006` carries reviewed request-protocol authority with arbitration and readiness still unobserved. `ECUM-007` and `ECUM-008` carry partial arbitration/action concepts with project rules, Action Lists and all runtime outcomes still open. `ECUM-003`, `ECUM-005` and `ECUM-009` carry partial configuration/communication procedures with project allocations and handoffs still undecided. `SURFACE_OR_ROLE_ONLY` rows carry role references with no procedure. `ECUM-002` and the nine `NO_EXPLICIT_REVIEWED_PRODUCT_PROCEDURE` rows carry documentation-scope outcomes, never capability verdicts. `ECUM-017` is project design by definition. `ECUM-018` records the full downstream chain as still required. All runtime verdicts are `NOT_EVALUATED`.
