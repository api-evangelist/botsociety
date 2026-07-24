---
name: Manage a Botsociety conversation
description: Create a conversation and populate it with messages, links, and variables using the legacy Botsociety apisociety 2.0 API.
api: openapi/botsociety-openapi.yml
operations:
  - createConversation
  - addMessage
  - linkMessage
  - addVariables
  - getConversations
---

# Manage a Botsociety conversation

Use this skill to build up a Botsociety design programmatically via the legacy
`apisociety/2.0/npm` API.

## Authentication
Send `user_id` and `api_key_public` headers on every request. See
`authentication/botsociety-authentication.yml`.

## Steps
1. **`createConversation`** — `POST /apisociety/2.0/npm/conversations/` with a conversation body.
   Keep the returned conversation `id`.
2. **`addMessage`** — `POST /apisociety/2.0/npm/conversations/{conversationId}/messages/` to add
   each message node.
3. **`linkMessage`** — `POST /apisociety/2.0/npm/conversations/{conversationId}/link` to connect two
   message nodes (`from` -> `to`). Use `unlinkMessage` to remove a connection.
4. **`addVariables`** — `POST /apisociety/2.0/npm/conversations/{conversationId}/variables/` to attach
   variables.
5. **`getConversations`** — `GET /apisociety/2.0/npm/conversations/{conversationId}` to read the
   assembled conversation back.

## Notes
- Content-Type is `application/json`; non-200 responses return a JSON error body.
- No idempotency key is supported — do not blindly retry writes. See
  `conventions/botsociety-conventions.yml`.
