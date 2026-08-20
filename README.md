# React Test Quality

`react-test-quality` is a Codex skill for designing, writing, strengthening, and reviewing trustworthy tests in React and JavaScript/TypeScript frontend projects.

Its purpose is not to maximize test count, snapshots, or line coverage. It helps a coding agent produce executable evidence that users and public consumers receive the promised behavior and that realistic regressions would be detected.

## Why this skill exists

A component test can render successfully and still prove almost nothing. Common false positives include:

- checking only that an element exists;
- clicking a test ID and verifying a mocked callback;
- mocking the component's own hook, client, provider, or essential child;
- asserting success without proving the request payload or server response;
- using broad snapshots instead of semantic outcomes;
- leaving promises, timers, handlers, stores, or caches shared between tests;
- using arbitrary waits that make race conditions likely instead of deterministic;
- treating coverage or mutation score as proof of user behavior.

This skill teaches the agent to recognize and avoid those patterns.

## Core philosophy

A good frontend test is an executable example of a user-facing or public contract. It establishes meaningful state, performs one coherent workflow, and checks observable consequences with an independently justified oracle.

The skill applies two complementary standards:

- **Bug-sensitive:** a realistic regression in the protected behavior makes the test fail.
- **Refactor-tolerant:** component extraction, hook rewrites, or state-management changes that preserve the contract keep the test passing.

Mutation testing supports this philosophy by sampling whether tests distinguish changed logic. It is a quality signal, not the definition of quality and not a reason to mutate incidental JSX merely to pursue 100%.

## What it covers

- User-centered and public-contract test design.
- Strong semantic assertions and independently derived expectations.
- Accessible queries through role, name, label, text, and visible value.
- `userEvent` workflows and correctly awaited interactions.
- Forms, validation, loading, success, empty, permission, and error behavior.
- Network interception that exercises real hooks, clients, normalization, and parsing.
- Request payload, URL, headers, cardinality, and forbidden-effect assertions.
- Fresh stores, query/cache clients, routers, sessions, fixtures, and handlers.
- Timers, deferred responses, cancellation, stale-response races, and optimistic rollback.
- Browser-layer decisions for routing, storage, downloads, focus, layout, streaming, and critical journeys.
- Vitest/Jest coverage interpretation and StrykerJS survivor triage.
- Detection of flaky tests, leaked state, weak oracles, and mocked-away behavior.
- Honest reporting of validation scope and residual risk.

## How the skill works

The entrypoint is [`SKILL.md`](SKILL.md). It gives the agent the essential workflow:

1. Discover the actual user or public contract.
2. Identify plausible regressions and meaningful states.
3. Choose the lowest test layer faithful to the risk.
4. Build fixtures and controlled responses that make wrong behavior observable.
5. Interact through the public surface and write a discriminating oracle.
6. Isolate async work, state, timers, network, storage, and caches.
7. Verify proportionally and report exactly what was proved.

Detailed guidance is loaded from `references/` only when relevant:

- `good-test-principles.md`: what makes a frontend test trustworthy.
- `react-test-layers.md`: choosing pure, component, network, hook, or browser tests.
- `assertions-fixtures-doubles.md`: semantic assertions, providers, fixtures, mocks, and snapshots.
- `async-state-isolation.md`: timers, requests, races, caches, routing, storage, and browser isolation.
- `mutation-and-metrics.md`: coverage and StrykerJS without metric gaming.
- `review-rubric.md`: blocking criteria for test-quality reviews.
- `sources.md`: primary documentation for tool configuration.

## When to use it

Invoke the skill when asking Codex to:

- write tests for a frontend feature or bug fix;
- review whether existing tests can produce false positives;
- strengthen a weak regression test;
- choose between pure, component, network, hook, and browser tests;
- improve state isolation or diagnose flakiness;
- test forms, permissions, loading, errors, retries, or race conditions;
- interpret coverage or mutation results;
- audit the quality of a React or JavaScript/TypeScript test suite.

It is intentionally not used merely to run an unchanged test suite.

## Installation

Install from GitHub with the Codex skill installer:

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --repo ThiagoCrepequer/react-test-quality \
  --path . \
  --ref main \
  --name react-test-quality
```

The skill is installed at:

```text
$CODEX_HOME/skills/react-test-quality
```

When `CODEX_HOME` is unset, Codex uses `~/.codex`, so the default path is `~/.codex/skills/react-test-quality`.

It becomes available to Codex on the next turn or session after installation.

## Invocation

Explicit invocation:

```text
$react-test-quality Write regression tests for this form and prove the request and visible outcome.
```

Other examples:

```text
$react-test-quality Review these component tests for false positives and leaked state.

$react-test-quality Design the correct component, network, and browser test boundaries for this flow.

$react-test-quality Triage these surviving StrykerJS mutants and strengthen only relevant behavior.
```

The skill also supports automatic selection when a request clearly concerns React or JavaScript/TypeScript test quality.

## Expected agent output

When work is complete, the agent should report:

- user/public contracts, states, and prohibited outcomes proved;
- why each test layer is faithful to the risk;
- exact commands, test counts, and results;
- mutation and coverage scope when those tools were run;
- justified survivors or exclusions;
- baseline failures, validations not run, and what the tests do not prove.

The result should be a test suite that fails for meaningful regressions, remains stable through behavior-preserving refactors, and communicates its confidence boundary honestly.
