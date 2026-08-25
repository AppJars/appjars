# Security Policy

## Reporting a vulnerability

Email **security@appjars.com**.

The authoritative version of this policy — including anything not covered here — is at
**https://www.appjars.com/security/**.

Please **do not** report a suspected vulnerability as an ordinary GitHub issue, in Discussions, or
through any other public channel until a fix has been released. A public report before a fix exists
puts every user of the affected AppJar at risk, including you.

Reports are accepted in English or Spanish.

## What to include

A useful report contains, at minimum:

- The affected AppJar and its exact version
- The Vaadin and Spring Boot versions in use
- What the vulnerability allows an attacker to do
- Steps or a minimal example that demonstrate it
- Any deployment conditions required (configuration, authentication state, exposed routes)
- A suggested mitigation, if you have one

## What to expect

We acknowledge every report within **5 business days**. After that you get our assessment, including
how we classify the issue, and updates while we work on it. When we publish an advisory we credit the
reporter, unless you would rather we did not.

We ask for a **90-day coordinated disclosure window**: 90 days from the day we acknowledge your
report, or until a fix is released, whichever comes first.

There is no bug bounty program.

## Supported versions

Security fixes are issued for the **latest released version of each AppJar**. We do not maintain
long-term support branches, so the remedy for a vulnerability in an older version is upgrading.

Supported Vaadin versions are listed in the documentation: https://docs.appjars.com

## Scope

**In scope:** the published AppJars artifacts under the `com.appjars` group ID, in supported versions.

**Out of scope:** your own application, third-party dependencies including Vaadin and Spring Boot, our
websites and documentation, the customer portal, and attempts to circumvent license checking. Report
third-party vulnerabilities to their respective maintainers.

The demo repositories are sample code rather than published artifacts. A security problem in the
sample code itself belongs in that demo's issue tracker. A problem in the AppJar that the demo
depends on goes to security@appjars.com.
