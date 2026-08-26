# Changelog

Every AppJar release, newest first. Each entry matches a
[GitHub release](https://github.com/AppJars/appjars/releases) and the artifacts published for that
version to `https://maven.appjars.com`.

Each AppJar has its own version number and its own release cadence; this file is the one place where
all of them are recorded together. Versions follow [semantic versioning](https://semver.org/): a
major version means the public API changed and an upgrade may require work on your side.

Every AppJar can be used free of charge. Free mode restricts how much you can run through it, and
holds some capabilities back for a licensed installation. Installing a license lifts the restrictions
with no code changes. What free mode allows for each AppJar is listed in the
[licensing documentation](https://docs.appjars.com/licensing/#free-mode-limits).

## Activity Log 2.0.0 — 2026-08-25

First public release of **Activity Log**.

Turn your application's log stream into a persistent, searchable audit trail. Define extraction rules
to capture the events that matter, give administrators a filterable view over them, and keep the data
bounded with retention policies.

Earlier versions of Activity Log have been released and are in production use. The version number
continues that history — what is new today is that releases are public.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer. The backend and service
layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/activity-log-2.0.0) ·
[Getting started](https://docs.appjars.com/activity-log/getting-started/) ·
[Documentation](https://docs.appjars.com/activity-log/overview/) ·
[Pricing](https://www.appjars.com/catalog/activity-log/)

