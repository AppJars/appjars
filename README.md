# AppJars

**AppJars** are modular, production-ready building blocks for enterprise Java applications, built on Spring Boot and Vaadin. Each AppJar covers one functional area — users, permissions, configuration, i18n, email, activity logging, and more — and drops into your own application instead of being rebuilt from scratch.

- Website: https://www.appjars.com
- Documentation: https://docs.appjars.com
- Catalog and pricing: https://www.appjars.com/catalog

Every AppJar can be used **free of charge** with limited functionality. A paid subscription unlocks the full feature set and includes updates for the subscription period. Details in the [catalog](https://www.appjars.com/catalog).

## What this repository is for

This repository contains **no source code**. It is the public issue tracker for every AppJar:

- **Bug reports** — something in an AppJar does not work as documented.
- **Feature requests** — something you would like an AppJar to do.

Free and paid users report through the same tracker and are treated the same way. Fixing bugs is part of the product, not a paid service.

It is also where releases are recorded. [CHANGELOG.md](CHANGELOG.md) lists every AppJar release, newest first, and each release is tagged in this repository.

## Where to go

| I want to… | Go to |
|---|---|
| Report a bug | [New issue → Bug report](../../issues/new/choose) |
| Request a feature | [New issue → Feature request](../../issues/new/choose) |
| Ask a question, or discuss anything | [AppJars Discussions](https://github.com/orgs/AppJars/discussions) |
| Report a security vulnerability | https://www.appjars.com/security/ |
| Get help with **my own** application | [Customer portal](https://customers.flowingcode.com) — human support and AI assistant, included with Startup and Enterprise |
| Read the documentation | https://docs.appjars.com |
| See what changed in a release | [CHANGELOG.md](CHANGELOG.md) |

See [SUPPORT.md](SUPPORT.md) for the full explanation of each channel.

## How issues are handled

Every new issue starts as `status/needs-triage`. Triage confirms the report, assigns the affected AppJar, and sets a status. Only `status/accepted` means we intend to act on it.

Issues are **closed when the fix is published in a release**, not when the code is merged, so that the state you see here matches something you can actually download and verify.

Bug fixes are scheduled by our own assessment of severity and impact. Issues carrying the **`Prioritized`** label have been escalated by an Enterprise subscriber and are taken first. See [SUPPORT.md](SUPPORT.md#issue-escalation-enterprise) for what escalation does and does not guarantee.

## Consuming AppJars

AppJars artifacts are published under the `com.appjars` group ID to our own Maven repository at
`https://maven.appjars.com`. Setup instructions are in the [documentation](https://docs.appjars.com).

## License

AppJars is a commercial product. Flowing Code S.A. owns and develops it; Flowing Code LLC is the licensor of record and distributor. Legal documents: https://www.appjars.com/legal/

The content of this repository (issue reports and discussion) is not covered by those documents — see [CONTRIBUTING.md](CONTRIBUTING.md) for how submitted reports and ideas are treated.
