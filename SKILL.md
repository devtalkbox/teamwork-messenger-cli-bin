---
name: teamwork-cli
description: Access Teamwork messaging features using the official CLI tool. Read conversations, messages, users, and networks; send text or file messages to DMs and groups. Requires the API URL and API token.
metadata:
  openclaw:
    emoji: "💬"
    requires:
      env:
        - "TEAMWORK_API_URL"
        - "TEAMWORK_API_TOKEN"
    primaryEnv: "TEAMWORK_API_TOKEN"
---

# Teamwork Messenger CLI Skill

Interact with the **Teamwork** messaging platform using its built-in Node.js CLI tool. This provides a simpler abstraction over the REST API without needing to handle `curl` payloads, tokens, or URL encoding.

## Configuration

The CLI relies on stateless authentication via environment variables.

| Variable | Description |
|---|---|
| `TEAMWORK_API_URL` | Base URL of the Teamwork backend (e.g. `https://teamwork.example.com`) |
| `TEAMWORK_API_TOKEN` | Your Teamwork API auth token |

Ensure the `teamwork` CLI command is available (either via a global install, `npm link`, or by running locally).

## CLI Operations

The `teamwork` CLI handles commands in logical categories: `auth`, `network`, `user`, and `chat`.

### Authentication

**View Current User Details**
Check the status of your current authenticated user. This displays your username, `tbId` (your sender ID), permission level, and displayName.
```bash
teamwork auth status
```
**Example Output:**
```text
┌──────────────────┬────────┬──────────────┬─────────────┐
│ username         │ tbId   │ permission   │ displayName │
├──────────────────┼────────┼──────────────┼─────────────┤
│ me@email.com     │ 1001   │ 2            │ Me          │
└──────────────────┴────────┴──────────────┴─────────────┘
```

### Network & Users

**List Networks**
View available networks that your account has access to.
```bash
teamwork network list
```
**Example Output:**
```text
┌─────────────┬──────────────────────────┐
│ networkId   │ name                     │
├─────────────┼──────────────────────────┤
│ 100         │ Test Message Network     │
└─────────────┴──────────────────────────┘
```

**List Users**
View all chatable users from the network.
```bash
teamwork user list
```
**Example Output:**
```text
┌───────────────────────────┬────────┬──────────────┬───────────────────┐
│ username                  │ tbId   │ permission   │ displayName       │
├───────────────────────────┼────────┼──────────────┼───────────────────┤
│ demoUser90000@email.com   │ 90000  │ 2            │ Demo User 90000   │
└───────────────────────────┴────────┴──────────────┴───────────────────┘
```

### Chat & Conversations 

**View Inbox**
Fetch recent conversations for the current user including unread message counts.
```bash
teamwork chat inbox
```
**Example Output:**
```text
┌─────────────────┬────────┬────────────────────┬───────────┐
│ ID              │ Type   │ Last Message       │ Unread    │
├─────────────────┼────────┼────────────────────┼───────────┤
│ 1101            │ User   │ Hello cool!!!!!    │ 0         │
└─────────────────┴────────┴────────────────────┴───────────┘
```

**Load Chat History**
Load message history of a specific conversation (user or group). 
- `<type>` must be `user` or `group`.
- `<conversation-id>` is the `tbId` of the target user/group.
- `[last-msg-id]` is an optional ID of the last message to load older messages from.

```bash
teamwork chat history <type> <conversation-id> [last-msg-id]
```
Example: `teamwork chat history user 1101`

**Example Output:**
```text
┌─────────┬──────────────┬─────────────┬─────────────────┐
│ Msg ID  │ Sender       │ Time        │ Content         │
├─────────┼──────────────┼─────────────┼─────────────────┤
│ 1000    │ 1101         │ 10:00 AM    │ Hello cool!!!!! │
└─────────┴──────────────┴─────────────┴─────────────────┘
```

**Send a Text Message**
Send a text message to a user or group.
```bash
teamwork chat send <type> <receiver-id> "Your message here"
```
Example: `teamwork chat send user 1101 "Hello world!"`

**Send a File or Image**
Upload and send a document or image to a user or group seamlessly.
```bash
teamwork chat send-file <type> <receiver-id> <file-path>
```
Example: `teamwork chat send-file group 2025 ./report.pdf`
