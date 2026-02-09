# Vapi MCP Server Setup

## Step 1: Get Your Vapi API Key

1. Go to the [Vapi Dashboard](https://dashboard.vapi.ai)
2. Navigate to account/API settings
3. Copy your API key

## Step 2: Add Vapi to Claude Desktop Config

Open `~/.claude.json` and add `vapi` to the `mcpServers` section alongside your existing Docker MCP Gateway:

```json
"mcpServers": {
  "MCP_DOCKER": {
    "command": "docker",
    "args": [
      "mcp",
      "gateway",
      "run"
    ]
  },
  "vapi": {
    "command": "npx",
    "args": ["-y", "@vapi-ai/mcp-server"],
    "env": {
      "VAPI_TOKEN": "YOUR_VAPI_API_KEY_HERE"
    }
  }
}
```

## Step 3: Restart Claude Desktop

Completely quit (Cmd+Q) and reopen. First launch will download the `@vapi-ai/mcp-server` package automatically.

## Step 4: Verify

Ask Claude: "List my Vapi assistants" - if it returns results (or an empty list), you're connected.

---

# Setting Up an Agent in Vapi

## Step 1: Create an Assistant

In the [Vapi Dashboard](https://dashboard.vapi.ai):

1. Go to Assistants
2. Create a new assistant
3. Paste your agent prompt (e.g., the contents of `franklin-m-theodore.md`) into the system prompt field

## Step 2: Configure Voice Settings

1. Choose a voice provider and voice for your assistant
2. Set the first message (what the assistant says when the call connects) or leave blank if your prompt handles the opening
3. Configure any other assistant settings (model, temperature, etc.)

## Step 3: Assign a Phone Number

1. Go to Phone Numbers in the dashboard
2. Buy or import a number
3. Assign your assistant to that number

## Step 4: Test

Use the Vapi Dashboard's built-in test call feature, or call the assigned phone number directly.

---

# Available MCP Tools

| Tool | What It Does |
|------|-------------|
| `vapi_list_assistants` | List all assistants |
| `vapi_get_assistant` | Get assistant by ID |
| `vapi_create_assistant` | Create new assistant |
| `vapi_update_assistant` | Update assistant |
| `vapi_delete_assistant` | Delete assistant |
| `vapi_list_calls` | List call history |
| `vapi_get_call` | Get call details |
| `vapi_create_call` | Make outbound call |
| `vapi_list_phone_numbers` | List phone numbers |
| `vapi_get_phone_number` | Get phone number details |
| `vapi_buy_phone_number` | Buy a phone number |
| `vapi_update_phone_number` | Update phone number config |
| `vapi_delete_phone_number` | Release a phone number |
