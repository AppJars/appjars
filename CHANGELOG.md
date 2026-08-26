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

