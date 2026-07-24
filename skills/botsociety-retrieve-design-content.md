---
name: Retrieve Botsociety design content
description: Fetch the messages, intents, and integration content of a Botsociety chatbot/voice-assistant design at runtime so a bot can serve up-to-date content without a code redeploy.
api: openapi/botsociety-openapi.yml
operations:
  - getConversation
---

# Retrieve Botsociety design content

Use this skill to pull the content of a Botsociety design (conversation) into a running
chatbot or voice assistant.

## Authentication
Every request needs two headers, both obtained from the Botsociety app:
- `user_id`
- `api_key_public`

Send them together on every call. See `authentication/botsociety-authentication.yml`.

## Steps
1. Obtain the design id (`conversationId`) from the Botsociety app.
2. Call **`getConversation`** — `GET /designs/{conversationId}/integrations` with the two auth headers.
3. Read the response: iterate `messages[]` (each has `id` and `path`) and, for NLP, read
   `intentsInfo` (intents, parameters, user/bot messages, bot responses).

## Notes
- Content-Type is `application/json`.
- On any non-200 the API returns a JSON error body; handle `401` (bad credentials) and
  `404` (unknown design). See `errors/botsociety-problem-types.yml`.
- There is no idempotency key or pagination; the full design content is returned. See
  `conventions/botsociety-conventions.yml`.
