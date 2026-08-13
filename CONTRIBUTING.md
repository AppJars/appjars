# Contributing

Thanks for taking the time to help make AppJars better. This page explains what contribution means here, because it is not the usual open source arrangement.

## Pull requests are not accepted

AppJars is a commercial product. Its source code lives in private repositories, and this repository contains no code. There is nothing to submit a pull request against, and we do not accept external code contributions.

Some subscriptions include access to source code for debugging purposes. That access does not carry the right to contribute, redistribute or publish modifications. See the license documents: https://www.appjars.com/legal/

## What is genuinely valuable to us

**Good bug reports.** A defect that we can reproduce in ten minutes gets fixed. A defect described as "it does not work" usually does not. The bug report form asks for versions, steps and a minimal reproducer for exactly this reason.

**Feature requests that describe a problem.** Tell us what you are trying to accomplish and why the current behaviour gets in the way. That is far more useful than a proposed implementation, because it lets us solve the problem in a way that fits the rest of the catalog.

**Answering other people in Discussions.** https://github.com/orgs/AppJars/discussions

## How to report well

1. Search first — open and closed issues both.
2. One report per issue. Three unrelated bugs in one issue cannot be triaged, scheduled or closed independently.
3. Use the forms. The required fields are the ones we need before we can even start.
4. A minimal reproducer beats any amount of description. A small project that fails on start is the single most effective thing you can attach.
5. Answer follow-up questions. Issues labelled `status/needs-info` are closed automatically after 14 days without a response, and can be reopened whenever the information arrives.

## Ideas you submit

By opening a feature request or posting an idea in Discussions, you agree that Flowing Code may implement, adapt, or decline it freely, in any AppJar or product, without compensation, attribution, or any obligation to you. You also confirm that you are free to share the idea — do not post anything covered by an agreement with a third party, and do not post confidential material belonging to your employer or your clients.

Nothing you post here grants you any right in AppJars, and nothing we do with a submitted idea creates any right for you in the resulting work.

## What we do with issues

Every issue starts as `status/needs-triage`. Triage assigns the affected AppJar, confirms or rejects the report, and sets one of:

| Label | Meaning |
|---|---|
| `status/accepted` | Confirmed, we intend to act on it |
| `status/needs-info` | We cannot proceed without more from you |
| `status/cannot-reproduce` | We tried and could not reproduce it |
| `status/not-a-bug` | Documented or intended behaviour |
| `status/duplicate` | Already tracked elsewhere; the link is in the comment |
| `status/wont-do` | Understood and declined, with a reason |
| `status/fixed-pending-release` | Fixed in code, not yet published |

Accepted issues may also carry a release target: `release/next-patch`, `release/next-minor` or `release/next-major` for the AppJar in question.

Issues are closed when the fix ships in a release, not when it is merged.

`status/wont-do` is a real answer and we will give it when it applies, with reasoning. It is more useful to you than an issue that stays open for two years.

## Be decent

Participation is covered by our [Code of Conduct](https://github.com/AppJars/.github/blob/main/CODE_OF_CONDUCT.md).
