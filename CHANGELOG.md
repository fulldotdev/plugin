# @fulldotdev/plugin

## 2.1.4

### Patch Changes

- aa23e8b: Every member of an organization has every app: `account_get` no longer lists apps per organization, and a refused call answers `FORBIDDEN` or `NOT_A_MEMBER`, no longer `NOT_ENTITLED`.
- aa23e8b: The skill says a task's comments, changes and links are its activity, now that a task has no notes of its own.
- 2f4de28: A new skill, website-review, reviews a website in a browser and puts its findings, with screenshots and recordings, in a shared scan report, on top with a note and a summary.

## 2.1.3

### Patch Changes

- 6d2869c: The login help, the skill and the plugin's description say an AI connection works in every organization you belong to, also ones you join later.
- 340f432: Website editing builds its fields from the website's content schema, without saved forms, and the website checks each save.
- 8fcbec5: The skill lets Fulldev's administrators change a customer organization's owner with `set_organization_owner`; everyone else still changes owners in the browser.

## 2.1.2

### Patch Changes

- a2ed575: The skill completes a task with what it delivered (`--results`) and changes a task's day, not its status, in its examples.

## 2.1.1

### Patch Changes

- c39fc20: The README installs Fulldev in Codex from OpenAI's plugin directory, the same plugin as in ChatGPT.

## 2.1.0

### Minor Changes

- 4803642: The plugin's descriptions, a first prompt and its review cases cover editing your website.
