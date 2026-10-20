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

## I18N Manager 3.1.0 — 2026-10-20

A feature release that helps translators get **MessageFormat** right before they save.

### Added

- Translation values are now **analyzed as they are edited**, in the grid editor and in the create
  dialog: a malformed pattern or an excessive length is reported as an error, a lone apostrophe in a
  parameterized value as a warning, and a doubled apostrophe without placeholders as a hint.
- The feedback explains **how many placeholders a single apostrophe hides** — the mistake
  MessageFormat itself cannot report, because the apostrophe quotes the rest of the value — and shows
  a **preview with sample values** alongside the count of placeholders in the text.
- **Learn more** now opens a dialog summarising the four rules a translator needs, each with what is
  typed and how it is shown, and links to the MessageFormat Javadoc as the full source. The examples
  are computed by MessageFormat itself, so they cannot drift from the actual behaviour.

### Fixes

- Braces hidden by a lone apostrophe are rejected, quoted braces that cannot be written unquoted are
  accepted, and an unclosed nested brace is reported as an error instead of throwing.
- The feedback popover closes when its field loses focus or is scrolled out of view, and the grid
  editor stays usable around it.
- The translation field keeps its label in the create dialog.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer, and appjars-utils 2.0.3.
The backend and service layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/i18n-manager-3.1.0) ·
[Getting started](https://docs.appjars.com/i18n-manager/getting-started/) ·
[Documentation](https://docs.appjars.com/i18n-manager/overview/) ·
[Pricing](https://www.appjars.com/catalog/i18n-manager/)

## Email Manager 2.1.0 — 2026-10-20

A feature release: **email templates**, a reusable subject and body with named placeholders, applied
to a new email from the compose form.

### Added

- A **template list view** at `em/templates`, with a WYSIWYG editor, an HTML source view, a
  placeholder palette with usage counts and a live preview, laid out for narrow screens.
- An **apply-template action** in the compose form, which renders the template and fills the subject,
  body and HTML flag. The email keeps no reference to the template it came from, and placeholder
  values are asked for when the template is applied.
- Templates are offered in the **best language variant** available when composing.
- **`PlaceholderCatalog`**, an optional SPI: an application publishes one or more beans to offer its
  own placeholder names in every template's palette.
- Two tables, `em_template` and `em_template_placeholder`, and the configuration properties
  `com.appjars.emailmanager.templates.max-body-size`, `max-rendered-size` and `locales`.

### Changed

- The flow artifact now depends on `org.parttio:hugerte-for-flow`, which carries the MIT-licensed
  HugeRTE editor and serves its JavaScript from the application's own `/assets/` path rather than a
  CDN. An application with a custom Spring Security configuration has to permit that path.
- The business artifacts now declare `org.jsoup:jsoup` directly. One sanitising policy is applied
  everywhere email HTML is shown, and it keeps the inline styles HTML email depends on.

### Fixes

- The **email list** is now reachable when no access rule matches its route.
- Template bodies are stored as written, every date type the renderer accepts is formatted, and the
  placeholders of a page of templates are loaded in one query.
- The editor keeps source edits when HTML is switched off, sends its content on change and blur, and
  keeps the last keystrokes when Save follows quickly.

Nothing in 2.0 changes: `EmailDto`, `em_email`, `EmailService` and the `EmailCrudView` constructor
are untouched, so an application that ignores templates sees no difference beyond the two new tables.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer, and appjars-utils 2.0.3.
The backend and service layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/email-manager-2.1.0) ·
[Getting started](https://docs.appjars.com/email-manager/getting-started/) ·
[Documentation](https://docs.appjars.com/email-manager/overview/) ·
[Pricing](https://www.appjars.com/catalog/email-manager/)

## AI Support 2.2.0 — 2026-10-20

A large release. The assistant now reaches beyond the application: the chat bubble can be embedded in
any website, it talks to Anthropic and Gemini models as well as OpenAI and Ollama, and it records,
hears and transcribes voice notes.

### Embedded chat

- The chat bubble is now published as the **`<ai-support-chat>` web component**, so it can be placed
  on any site — a static marketing page included — and answered from the application like any other
  conversation.
- **Web channels** tie each embedding site to an assistant. Only a site with an enabled web channel
  can load the chat, and turning the channel off takes the chat off the site.
- Visitors are anonymous: each browser gets its own cookie and is named `visitor-` plus a short hash.
- The embedded chat is built in the **embedding page's language**, sends the page's context with each
  message, and can be dragged to a corner, which it remembers.
- Hosts can **switch off optional features** and suppress notifications, and the chat works inside a
  shadow root.
- Visitor sessions are purged after a while, with bounds on how many messages a visitor sends and on
  the length of messages and context.
- Setup: serve it from a host on the site's own domain, let `/web-component/**` through the security
  configuration, and have Vaadin scan `com.appjars.aisupport.flow.embed`. The README has the full
  procedure.

### Models and providers

- **Anthropic and Gemini models** are now supported, alongside OpenAI, OpenAI-compatible servers and
  Ollama.
- Each LLM now stores **the content types its model accepts**, prefilled from a built-in model
  catalog and editable in the LLM form.
- An LLM's configuration can be **tested from its form**.
- An attachment a model does not accept is now sent as text, or as a note when it cannot be.
- Token estimates now cover OpenAI models the tokenizer does not know.

### Voice notes and transcription

- Users can **record and play voice notes** where the chat offers attachments.
- Audio is **transcribed by the system LLM** for models that do not hear it, and the transcript is
  stored with the attachment, shown under the audio, and used wherever the text of a message is read
  — retrieval, moderation and the session summary.
- Audio is sent in the formats each provider reads, and its tokens are estimated by how long it
  plays.

### Attachments and chat memory

- The chat now accepts **Markdown, CSV and Excel** attachments.
- Documents a model does not read are sent as their text, long PDFs included, with PDF pages capped
  per turn.
- A turn's attachments are **fitted to a token budget**, and the uploader is told when text was cut.
  Administrators are told when a channel attachment could not be fully read.
- The memory budget now defaults to **25,000 tokens**, and a turn the model rejected is kept out of
  the memory.
- Model errors reach the inspector with their reason and **without credentials or quoted secrets**.

### Private messages and session summaries

- Every assistant prompt is now **wrapped in fixed rules**, and private messages are kept out of
  answers everybody sees and out of users' message search.
- Administrators can send **private messages from the chat bubble**, and switch a session between
  automatic and manual mode.
- Session summaries are now generated **in batches** on their own executor, instead of after every
  answer.

### Channels

- Host applications can now **add channel types of their own**, with no persistence code.
- Repeated or concurrent channel messages are kept in one session, a channel is deleted and its
  sessions unlinked in one transaction, and WhatsApp Coexistence echoes are read as the business's
  own messages.
- Replies longer than a channel accepts are sent in parts, a channel is marked failed when its
  provider answers 401 or rejects an upload, and WhatsApp media is streamed so the size limit stops
  large files.

### Administration views on phones

- The administration views, filters, dialogs, content viewer, vector search, inspector and tools
  picker now **fit on phones**, with dialogs shown full screen and a row's hidden columns shown on a
  tap.
- Session and message search results are shown in tabs with their counts, the extra document actions
  are gathered in a menu, and the message input's actions collapse into an overflow menu.

### Fixes

- The embedding store database now defaults to `spring.datasource.url`.
- Enum columns no longer generate CHECK constraints, and the logging backend is left to the host
  application.
- AI Support starts without an application `UserProfilePictureProvider`, and the queries of the
  largest tables are indexed.

### Upgrading

Databases created by earlier versions keep check constraints and a narrow configuration column that
`ddl-auto=update` never changes. Run once, before creating an Anthropic or Gemini LLM, a web channel
or a channel of your own type:

```sql
ALTER TABLE as_llm DROP CONSTRAINT IF EXISTS as_llm_type_check;
ALTER TABLE as_llm_exchange DROP CONSTRAINT IF EXISTS as_llm_exchange_llm_type_check;
ALTER TABLE as_llm ALTER COLUMN configuration TYPE text;
ALTER TABLE as_channel DROP CONSTRAINT IF EXISTS as_channel_channel_type_check;
```

Transcripts are stored in the new `transcript` column of `as_message_attachment`, which
`ddl-auto=update` adds; a schema managed otherwise needs it added once.

- `memory.max-tokens` now defaults to `25000` instead of `10000`. Set it to `10000` to keep the
  previous size, and lower it for a small-context model.
- Answering no longer regenerates the session summary. The chat views request summaries themselves;
  code that adds messages outside them calls `AssistantService.summarizeSession`.
- `ChannelService`, `ChannelDao`, `MessageAttachmentService` and `MessageAttachmentDao` gain methods.
  Applications that implement any of these interfaces themselves must implement them.
- A session open before the upgrade keeps the private messages its memory already holds until it is
  closed. `DELETE FROM as_chat_memory` clears them right away, at the cost of the earlier context of
  those conversations.
- The enum-typed channel accessors and `PromptDto.system` are deprecated; `ChannelDto.getType()`
  returns the type key of every channel.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer, and appjars-utils 2.1.0.
The backend and service layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/ai-support-2.2.0) ·
[Getting started](https://docs.appjars.com/ai-support/getting-started/) ·
[Documentation](https://docs.appjars.com/ai-support/overview/) ·
[Pricing](https://www.appjars.com/catalog/ai-support/)

## User Manager 2.0.2 — 2026-09-29

A patch release that creates the anonymous authority at startup.

### Fixes

- The **anonymous authority** is now created at startup when it is missing, so an installation that
  adopts User Manager over an existing user table has it from the first anonymous visit.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer, and appjars-utils 2.0.3.
The backend and service layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/user-manager-2.0.2) ·
[Getting started](https://docs.appjars.com/user-manager/getting-started/) ·
[Documentation](https://docs.appjars.com/user-manager/overview/) ·
[Pricing](https://www.appjars.com/catalog/user-manager/)

## Process Manager 2.0.1 — 2026-09-29

A patch release, covering listener lifecycle in the process list.

### Fixes

- **Resize listeners** are now released when the process list view detaches.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer, and appjars-utils 2.0.3.
The backend and service layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/process-manager-2.0.1) ·
[Getting started](https://docs.appjars.com/process-manager/getting-started/) ·
[Documentation](https://docs.appjars.com/process-manager/overview/) ·
[Pricing](https://www.appjars.com/catalog/process-manager/)

## Issue Tracker 2.0.2 — 2026-09-29

A patch release, covering uploads, saved filters, project activity and user pickers.

### Fixes

- **File uploads** in custom fields and CSV imports now use the upload handler API, one file at a
  time.
- In the **CSV import**, **Next** is available only while a non-empty file is uploaded, and starting
  another import clears the headers of the previous one.
- Saved queries now keep the values of the **Assignee's group** filter.
- **Project activity** now reads activity timestamps in every type the database driver returns.
- **User pickers** now handle installations without the anonymous user.

### API note

`CustomFieldUploadComponent.setAcceptedFileTypes(String...)` now takes file extensions with their
leading dot, such as `.png`, and raises an `IllegalArgumentException` for a MIME type.
`UserService.findAnonymousUser()` returns `null` when the anonymous user does not exist.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer, and appjars-utils 2.0.3.
The backend and service layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/issue-tracker-2.0.2) ·
[Getting started](https://docs.appjars.com/issue-tracker/getting-started/) ·
[Documentation](https://docs.appjars.com/issue-tracker/overview/) ·
[Pricing](https://www.appjars.com/catalog/issue-tracker/)

## I18N Manager 3.0.1 — 2026-09-29

A patch release, covering listener lifecycle in the views.

### Fixes

- **Resize listeners** are now scoped to the component that registers them and released when it
  detaches.

**Requires** Java 21, Spring Boot 4.x, and Vaadin 25.2 for the UI layer, and appjars-utils 2.0.3.
The backend and service layers of an AppJar do not require Vaadin.

[Release](https://github.com/AppJars/appjars/releases/tag/i18n-manager-3.0.1) ·
[Getting started](https://docs.appjars.com/i18n-manager/getting-started/) ·
[Documentation](https://docs.appjars.com/i18n-manager/overview/) ·
[Pricing](https://www.appjars.com/catalog/i18n-manager/)

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

