# Security Policy

## Reporting a vulnerability

If you believe you have found a security vulnerability in any AppJar, follow the process described at:

**https://www.appjars.com/security/**

That page is the authoritative source for how to reach us, what to include in a report, and what to expect afterwards.

Please **do not** report suspected vulnerabilities as ordinary GitHub issues or in Discussions until they have been addressed and a fix has been released. A public report before a fix exists puts every user of the affected AppJar at risk, including you.

## What to include

A useful report contains, at minimum:

- The affected AppJar and its exact version
- The Vaadin, Spring Boot and Java versions in use
- What the vulnerability allows an attacker to do
- Steps or a minimal example that demonstrate it
- Any deployment conditions required (configuration, authentication state, exposed routes)

## Supported versions

Security fixes are issued for AppJar versions covered by a current subscription period, on the Vaadin versions listed as supported in the documentation: https://docs.appjars.com

Versions built against Vaadin releases that are no longer supported do not receive fixes. If a report affects an unsupported version, the remedy is upgrading.

## Scope

This policy covers the AppJars libraries themselves. It does not cover vulnerabilities in your own application, in Vaadin, in Spring Boot, or in other third-party dependencies — those should be reported to their respective maintainers.
