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

## Email Manager 2.0.2 — 2026-09-29

A patch release that changes who can open the email list.

### Upgrading

The **Emails** view now opens for any authenticated user, and it lists every email. If only some
roles should manage emails, restrict the view through your application's security configuration, for
example with a User Manager access rule on its route.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer, and appjars-utils 2.0.3.
The backend and service layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/email-manager-2.0.2) ·
[Getting started](https://docs.appjars.com/email-manager/getting-started/) ·
[Documentation](https://docs.appjars.com/email-manager/overview/) ·
[Pricing](https://www.appjars.com/catalog/email-manager/)

## Dynamic Menu 2.1.0 — 2026-09-29

A minor release, focused on how the free mode allowance is counted.

### Free mode

- **Separators**, **items without a URL** and **items that open a view of an AppJar** no longer
  count towards the five-item allowance, so it is kept for the entries of your own views.
- **New item** and **Import** stay available at the limit. The item editor and the import dialog
  disable **Save** only when the result would exceed the allowance, and the import projection
  follows the selected strategy.

### Fixes

- The **item editor** now keeps an icon family that the application no longer offers when the item
  is saved.

### API note

`MenuItemService` adds three abstract methods, along with the `FreeLimitStatus` record they use:

- `getFreeLimitStatus()`
- `canSaveWithinFreeLimit(MenuItemDto)`
- `canImportWithinFreeLimit(List<MenuItemDto>, ImportStrategy)`

An application that implements the interface itself must implement them when upgrading.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer, and appjars-utils 2.0.2.
The backend and service layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/dynamic-menu-2.1.0) ·
[Getting started](https://docs.appjars.com/dynamic-menu/getting-started/) ·
[Documentation](https://docs.appjars.com/dynamic-menu/overview/) ·
[Pricing](https://www.appjars.com/catalog/dynamic-menu/)

## Data Query 1.0.1 — 2026-09-29

A patch release, covering REST request tests and the grid export.

### Fixes

- **Test request** now runs in the background, with a loading indicator in the **Request result**
  dialog.
- The **grid export** footer is now opaque on Vaadin 25.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer, and appjars-utils 2.0.2.
The backend and service layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/data-query-1.0.1) ·
[Getting started](https://docs.appjars.com/data-query/getting-started/) ·
[Documentation](https://docs.appjars.com/data-query/overview/) ·
[Pricing](https://www.appjars.com/catalog/data-query/)

## Configuration Manager 2.0.1 — 2026-09-29

A patch release, covering listener lifecycle in the views.

### Fixes

- **Resize listeners** are now scoped to the component that registers them and released when it
  detaches.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer, and appjars-utils 2.0.3.
The backend and service layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/configuration-manager-2.0.1) ·
[Getting started](https://docs.appjars.com/configuration-manager/getting-started/) ·
[Documentation](https://docs.appjars.com/configuration-manager/overview/) ·
[Pricing](https://www.appjars.com/catalog/configuration-manager/)

## AI Support 2.1.0 — 2026-09-29

A minor release. Tools are now assigned per assistant, the chat memory keeps long conversations
within a token budget, and the LLM Inspector shows what tools cost.

### Tools per assistant

Each assistant now receives only the tools assigned to it, from a new **Tools** tab in the assistant
dialog. An administrator can assign a whole class, which includes the tools added to it later, or
individual tools. `appjars.aisupport.tooling.allowedPackages` now bounds which tools can be
assigned.

### Chat memory

- The chat memory is now a **token window with a running summary**: older turns are folded into the
  summary instead of being dropped, so the context of a long conversation survives.
- Compaction runs **in the background** once the answer has been delivered.
- **Attachments** are kept by reference, and the most recent ones stay available as they were sent.
- New `appjars.aisupport.memory.*` properties set the budgets. Their defaults derive from
  `appjars.aisupport.memory.max-tokens`, so one property is enough to resize the memory.
- The summarizer has its own `appjars.aisupport.memory.summarize.timeout`, and
  `com.appjars.aisupport.models.timeout` no longer applies to it.

### LLM Inspector

- Each exchange shows the **tools offered** to the model, the **calls** it made with their arguments
  and results, the tokens the tools cost, and the number of model calls.
- The LLM row shows the model type and name.

### Chat experience

- The **mention list** leads with the role calls, shows each person's name above the username it
  types, and says when more users match.
- The **participant list** shows the username under each name.
- **Mentioning the assistant** in a manual conversation now passes that message to the model.
- The Chat, LLM Inspector, Assistants and LLMs views accept **filters as URL query parameters**, so
  a filtered view can be linked to directly.

### Messaging channels

A message from a contact whose previous session is closed or archived now **opens a new session**,
and the previous one stays as the record of that conversation.

### Fixes

- **Prompt overrides** placed under `/prompts` now apply to background tasks as well when the
  application runs from a Spring Boot jar.

### Upgrading

Tools used to be available to every assistant. Assignments are not created on upgrade, so existing
assistants start with no tools: open each assistant and assign its tools in the **Tools** tab.
**Select all** restores the previous behaviour for that assistant.

### API changes

- `ToolCatalogService` exposes the discovered tools, and `AssistantDto.getToolAssignments()` carries
  the assignments of an assistant as `ToolAssignmentDto` records.
- `UserProfilePictureProvider` adds `getDisplayNameByUsername(String)`, an optional default method
  that supplies the name shown in the mention and participant lists.
- `LlmExchangeDto.getLlmContent()` is deprecated for removal and always returns `null`. Use
  `getLlmId()`, `getLlmName()` and `getLlmType()` to identify the model.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer, and appjars-utils 2.0.3.
The backend and service layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/ai-support-2.1.0) ·
[Getting started](https://docs.appjars.com/ai-support/getting-started/) ·
[Documentation](https://docs.appjars.com/ai-support/overview/) ·
[Pricing](https://www.appjars.com/catalog/ai-support/)

## Activity Log 2.1.0 — 2026-09-29

A minor release, with refinements to the extractor and remover views.

### Extractors and removers

- The **name filter** of the extractor and remover lists now applies when Enter is pressed.
- A failed save now shows its error **next to the affected field**, reports an empty logger or
  detail filter section under its own grid, and scrolls to the first section with an error.

### Fixes

- **Resize listeners** are now scoped to the component that registers them and released when it
  detaches.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer, and appjars-utils 2.0.3.
The backend and service layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/activity-log-2.1.0) ·
[Getting started](https://docs.appjars.com/activity-log/getting-started/) ·
[Documentation](https://docs.appjars.com/activity-log/overview/) ·
[Pricing](https://www.appjars.com/catalog/activity-log/)

## User Profile 2.0.1 — 2026-09-08

A patch release, covering the avatar upload and listener lifecycle in the views.

### Fixes

- **Avatar upload** now uses the upload handler API.
- **Resize listeners** are now scoped to the view that registers them and released when it detaches.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer. The backend and service
layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/user-profile-2.0.1) ·
[Getting started](https://docs.appjars.com/user-profile/getting-started/) ·
[Documentation](https://docs.appjars.com/user-profile/overview/) ·
[Pricing](https://www.appjars.com/catalog/user-profile/)

## User Manager 2.0.1 — 2026-09-08

A patch release, with fixes to the access rule dialog, registration links, and listener lifecycle in
the views.

### Fixes

- The **access rule editing dialog** now keeps its delete button available, whether or not the
  creation dialog was opened earlier in the same session.
- **Registration link conversion** now handles lazy proxies.
- **Resize listeners** are now scoped to the component that registers them — the view in routed
  views, the dialog in the rule dialog, and the row detail layout in the users, groups, rules and
  views lists — and released when it detaches.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer. The backend and service
layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/user-manager-2.0.1) ·
[Getting started](https://docs.appjars.com/user-manager/getting-started/) ·
[Documentation](https://docs.appjars.com/user-manager/overview/) ·
[Pricing](https://www.appjars.com/catalog/user-manager/)

## Issue Tracker 2.0.1 — 2026-09-08

A patch release that tightens listener lifecycle across the views.

### Fixes

- **Resize listeners** are now scoped to the component that registers them and released when it
  detaches.
- **Custom query save listeners** are now owned by each subscriber, registered on attach and removed
  on detach, and kept across saves and cancels, so every attached component is notified of every
  save.

### API note

`CustomQueryDialog.addCustomQuerySaveListener` now returns a `Registration` instead of `void`. Calls
that ignore the result keep compiling; recompile against 2.0.1.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer. The backend and service
layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/issue-tracker-2.0.1) ·
[Getting started](https://docs.appjars.com/issue-tracker/getting-started/) ·
[Documentation](https://docs.appjars.com/issue-tracker/overview/) ·
[Pricing](https://www.appjars.com/catalog/issue-tracker/)

## Email Manager 2.0.1 — 2026-09-08

A patch release, covering attachment uploads and listener lifecycle in the views.

### Fixes

- **Attachment upload** now uses the upload handler API. Each upload is read into a bounded buffer,
  and the retained count and reported MIME type are validated before anything is stored, so an
  invalid or unreadable upload is rejected and no temporary file is left behind.
- **Resize listeners** are now scoped to the view that registers them and released when it detaches.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer. The backend and service
layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/email-manager-2.0.1) ·
[Getting started](https://docs.appjars.com/email-manager/getting-started/) ·
[Documentation](https://docs.appjars.com/email-manager/overview/) ·
[Pricing](https://www.appjars.com/catalog/email-manager/)

## AI Support 2.0.1 — 2026-09-08

A patch release, with fixes to document categories, the chat bubble, and listener lifecycle in the
views.

### Fixes

- Documents assigned to **more than one category** are now retrieved when filtering by any of them.
- The **category metadata backfill** — which repairs the metadata of embeddings uploaded before this
  release — now runs once the application is ready, with its error boundary outside the transaction,
  so a failure is reported without affecting the host application. Its query no longer depends on the
  `?` jsonb operator, which is read as a parameter placeholder in some setups.
- **Embedding metadata storage** is now pinned to `jsonb`, so the embedding store always agrees with
  the entity mapping rather than depending on bean initialization order.
- The **chat bubble** now handles an installation with no assistant configured: the message input
  stays disabled and the send pipeline guards the case.
- **Lazy channel proxies** are now unwrapped before conversion.
- **Resize listeners** are now scoped to the view that registers them and released when it detaches.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer. The backend and service
layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/ai-support-2.0.1) ·
[Getting started](https://docs.appjars.com/ai-support/getting-started/) ·
[Documentation](https://docs.appjars.com/ai-support/overview/) ·
[Pricing](https://www.appjars.com/catalog/ai-support/)

## User Profile 2.0.0 — 2026-08-25

First public release of **User Profile**.

Ready-made views for users to manage their own details, with avatar upload and cropping built in,
plus an administration view for centralised oversight.

Earlier versions of User Profile have been released and are in production use. The version number
continues that history — what is new today is that releases are public.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer. The backend and service
layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/user-profile-2.0.0) ·
[Getting started](https://docs.appjars.com/user-profile/getting-started/) ·
[Documentation](https://docs.appjars.com/user-profile/overview/) ·
[Pricing](https://www.appjars.com/catalog/user-profile/)

## User Manager 2.0.0 — 2026-08-25

First public release of **User Manager**.

The cornerstone of application security: users, roles and hierarchical groups, with granular access
rules protecting views and URLs, plus built-in workflows for registration, password recovery and
security policy enforcement.

Earlier versions of User Manager have been released and are in production use. The version number
continues that history — what is new today is that releases are public.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer. The backend and service
layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/user-manager-2.0.0) ·
[Getting started](https://docs.appjars.com/user-manager/getting-started/) ·
[Documentation](https://docs.appjars.com/user-manager/overview/) ·
[Pricing](https://www.appjars.com/catalog/user-manager/)

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

