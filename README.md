## User Guide & Commands

The CLI organizes commands into categories: `auth`, `network`, `user`, and `chat`. 

### Authentication Commands

**View Current User Details**
Check the status of your current authenticated user.
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

### Network & User Commands

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

### Chat Commands

**View Inbox**
Fetch recent conversations for the current user.
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
```bash
teamwork chat history <type> <conversation-id> [last-msg-id]
```
**Example Output:**
```text
┌─────────┬──────────────┬─────────────┬─────────────────┐
│ Msg ID  │ Sender       │ Time        │ Content         │
├─────────┼──────────────┼─────────────┼─────────────────┤
│ 1000    │ 1101         │ 10:00 AM    │ Hello cool!!!!! │
└─────────┴──────────────┴─────────────┴─────────────────┘
```
- `<type>`: `user` or `group`
- `<conversation-id>`: The ID of the user or group.
- `[last-msg-id]`: (Optional) ID of the last message to load older messages from.

**Send a Text Message**
Send a text message to a user or group.
```bash
teamwork chat send <type> <receiver-id> "Your message here"
```
- `<type>`: `user` or `group`
- `<receiver-id>`: the ID of the target user or group.

**Send a File or Image**
Upload and send a document or image to a user or group.
```bash
teamwork chat send-file <type> <receiver-id> <file-path>
```
- `<type>`: `user` or `group`
- `<receiver-id>`: the ID of the target user or group
- `<file-path>`: The path to the local file to upload.
