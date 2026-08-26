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

## Process Manager 2.0.0 — 2026-08-25

First public release of **Process Manager**.

Orchestrate, schedule and monitor background jobs. Users can trigger a process immediately or
schedule it for later, and every execution is kept with its history.

Earlier versions of Process Manager have been released and are in production use. The version number
continues that history — what is new today is that releases are public.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer. The backend and service
layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/process-manager-2.0.0) ·
[Getting started](https://docs.appjars.com/process-manager/getting-started/) ·
[Documentation](https://docs.appjars.com/process-manager/overview/) ·
[Pricing](https://www.appjars.com/catalog/process-manager/)

## Issue Tracker 2.0.0 — 2026-08-25

First public release of **Issue Tracker**.

Embed a complete issue tracking system inside your own application. Manage projects, tickets, custom
workflows and time tracking without sending users to an external tool, and keep the data in your own
database.

Earlier versions of Issue Tracker have been released and are in production use. The version number
continues that history — what is new today is that releases are public.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer. The backend and service
layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/issue-tracker-2.0.0) ·
[Getting started](https://docs.appjars.com/issue-tracker/getting-started/) ·
[Documentation](https://docs.appjars.com/issue-tracker/overview/) ·
[Pricing](https://www.appjars.com/catalog/issue-tracker/)

## I18N Manager 3.0.0 — 2026-08-25

A major release, built on a reorganisation of the module's public API.

### Locale handling

- The UI locale is now **resolved from the browser's language preferences** on each page load, so a
  visitor sees your application in their own language without any configuration
- **Manual locale controls** are exposed for applications that let users choose explicitly

### Translation workflow

- Scanning for missing keys can now **load them from the parent language**, so a regional variant
  starts from its base language instead of from nothing
- Refinements throughout the language and translation views

### API changes

Flow classes have moved from `com.appjars.i18nmanager.vaadin.*` to `com.appjars.i18nmanager.flow.*`,
aligning I18N Manager with the package layout used across the catalog. **This is the change that
makes 3.0.0 a major release.**

To upgrade, update the imports in your application:

```
com.appjars.i18nmanager.vaadin.  →  com.appjars.i18nmanager.flow.
```

If you list AppJars packages in `vaadin.allowed-packages`, update that entry too.

Alongside the move, the public surface has been tightened: implementation classes are no longer
exposed, and the DTO and serialization contracts are stricter. Applications using the documented API
are unaffected.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer. The backend and service
layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/i18n-manager-3.0.0) ·
[Getting started](https://docs.appjars.com/i18n-manager/getting-started/) ·
[Documentation](https://docs.appjars.com/i18n-manager/overview/) ·
[Pricing](https://www.appjars.com/catalog/i18n-manager/)

## Email Manager 2.0.0 — 2026-08-25

First public release of **Email Manager**.

Decouple writing an email from sending it. Messages are queued in your database, sent asynchronously,
retried automatically when delivery fails, and kept with their full delivery history.

Earlier versions of Email Manager have been released and are in production use. The version number
continues that history — what is new today is that releases are public.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer. The backend and service
layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/email-manager-2.0.0) ·
[Getting started](https://docs.appjars.com/email-manager/getting-started/) ·
[Documentation](https://docs.appjars.com/email-manager/overview/) ·
[Pricing](https://www.appjars.com/catalog/email-manager/)

## Dynamic Menu 2.0.0 — 2026-08-25

First public release of **Dynamic Menu**.

Build multi-level navigation that is defined at runtime rather than hardcoded, with visibility
filtered automatically by each user's permissions.

Earlier versions of Dynamic Menu have been released and are in production use. The version number
continues that history — what is new today is that releases are public.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer. The backend and service
layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/dynamic-menu-2.0.0) ·
[Getting started](https://docs.appjars.com/dynamic-menu/getting-started/) ·
[Documentation](https://docs.appjars.com/dynamic-menu/overview/) ·
[Pricing](https://www.appjars.com/catalog/dynamic-menu/)

## Data Query 1.0.0 — 2026-08-25

First public release of **Data Query**.

Turn stored queries into complete reporting screens without writing Java or redeploying. Define a
query once and Data Query generates the parameter form, the results grid, the charts and the
drill-down navigation — plus dashboards and pixel-accurate PDF reports designed in a visual editor.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer. The backend and service
layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/data-query-1.0.0) ·
[Getting started](https://docs.appjars.com/data-query/getting-started/) ·
[Documentation](https://docs.appjars.com/data-query/overview/) ·
[Pricing](https://www.appjars.com/catalog/data-query/)

## Configuration Manager 2.0.0 — 2026-08-25

First public release of **Configuration Manager**.

Manage global and per-user settings at runtime, without touching a properties file or redeploying.
Every change is recorded with a full audit history of who changed what, and when.

Earlier versions of Configuration Manager have been released and are in production use. The version
number continues that history — what is new today is that releases are public.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer. The backend and service
layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/configuration-manager-2.0.0) ·
[Getting started](https://docs.appjars.com/configuration-manager/getting-started/) ·
[Documentation](https://docs.appjars.com/configuration-manager/overview/) ·
[Pricing](https://www.appjars.com/catalog/configuration-manager/)

## AI Support 2.0.0 — 2026-08-25

A large release. AI Support grows from a chat assistant over your documents into a full support
channel, with messaging integrations, richer retrieval, and prompt management.

### Messaging channels

Conversations no longer have to start inside your application. AI Support now receives and replies to
messages from **WhatsApp**, **Facebook Messenger** and **Instagram**, with attachments supported in
both directions, and every channel managed from a single unified view.

### Documents and retrieval

- **Vector search** over your document library, directly from the documents view
- **Document metadata** — store your own alongside any document, and view what was extracted
- **Chunk templates** for controlling how a document is prepared for retrieval
- **Retrieval detail** captured with each exchange, so you can see which chunks and queries produced
  an answer
- **Token estimates** for documents, messages and prompts

### Prompts

Prompts are now versioned. Every edit is recorded, the full revision history is available from the
prompts view, and previous versions can be reviewed side by side with a diff.

### Chat experience

- **File attachments** in chat, with inline image previews
- **Markdown rendering**, including Mermaid diagrams
- **Mobile layout** and a resizable assistant window
- **Private mode** for messages that stay out of the conversation
- Search that scrolls directly to the matching message
- Live updates across every view as data changes

### Extensibility

- **Tool support**, with automatic scanning of the tools you expose
- **Authentication provider SPI** for plugging in your own identity source
- **Session summaries** through a provider interface, with a default implementation

### Upgrading

This is a major release, and the public API has moved on since 1.0.0. Review the getting started
guide before upgrading, and expect to revisit your configuration.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer. The backend and service
layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/ai-support-2.0.0) ·
[Getting started](https://docs.appjars.com/ai-support/getting-started/) ·
[Documentation](https://docs.appjars.com/ai-support/overview/) ·
[Pricing](https://www.appjars.com/catalog/ai-support/)

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

