# Notebooks and API usage

- Secrets: the API key lives in `.env` (gitignored). Load with `load_dotenv(override=True)`. Never print, hardcode or commit keys.
- SDK: `from anthropic import Anthropic`; `client.messages.create(...)`.
- Model IDs: use current ones (the notebook uses `claude-sonnet-4-6`); check the `claude-api` skill rather than guessing IDs.
- Conversations: keep a `messages` list of `{"role", "content"}` dicts and append user/assistant turns via helper functions (`add_message`, `chat_with_claude`).
- Temperature: 0.0–1.0; low = deterministic, high = creative.
- Clear notebook outputs that contain sensitive data before committing.
- Edit notebooks with NotebookEdit, not by hand-editing JSON.
