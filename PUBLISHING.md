# Publishing to the official MCP Registry

This repo publishes metadata (`server.json`) to the [official MCP Registry](https://registry.modelcontextprotocol.io)
under the domain-verified namespace **`com.surveysparrow`**. The registry stores only metadata — it points clients
at our already-hosted endpoint (`https://integrations.surveysparrow.com/surveysparrow/mcp`).

> **Why domain auth:** the `com.surveysparrow/*` namespace is proven by ownership of `surveysparrow.com`.
> It also requires the server's remote URL to be on `surveysparrow.com` or a subdomain — `integrations.surveysparrow.com` qualifies.

## Prerequisites

- Ability to add a DNS TXT record at the **`surveysparrow.com` apex**, **or** to serve a file at
  `https://surveysparrow.com/.well-known/mcp-registry-auth` (either one proves domain ownership).
- `openssl` and the `mcp-publisher` CLI.

## 1. Install the `mcp-publisher` CLI

```bash
brew install mcp-publisher
```

Or download a prebuilt binary:

```bash
curl -L "https://github.com/modelcontextprotocol/registry/releases/latest/download/mcp-publisher_$(uname -s | tr '[:upper:]' '[:lower:]')_$(uname -m | sed 's/x86_64/amd64/;s/aarch64/arm64/').tar.gz" | tar xz mcp-publisher \
  && sudo mv mcp-publisher /usr/local/bin/
```

## 2. Generate an Ed25519 key pair

```bash
openssl genpkey -algorithm Ed25519 -out key.pem
PUBLIC_KEY="$(openssl pkey -in key.pem -pubout -outform DER | tail -c 32 | base64)"
```

> ⚠️ `key.pem` is a **private key**. It is git-ignored in this repo — never commit it.

## 3. Prove domain ownership (pick ONE)

**Option A — DNS TXT record** at the `surveysparrow.com` apex (not a subdomain):

```bash
echo "surveysparrow.com. IN TXT \"v=MCPv1; k=ed25519; p=${PUBLIC_KEY}\""
```

Add the printed `v=MCPv1; ...` value as a TXT record and wait for it to propagate.

**Option B — HTTP well-known file** served at `https://surveysparrow.com/.well-known/mcp-registry-auth`:

```bash
echo "v=MCPv1; k=ed25519; p=${PUBLIC_KEY}"
```

Serve exactly that line as the file body.

## 4. Log in

```bash
PRIVATE_KEY="$(openssl pkey -in key.pem -noout -text | grep -A3 "priv:" | tail -n +2 | tr -d ' :\n')"

# If you used the DNS TXT record:
mcp-publisher login dns  --domain surveysparrow.com --private-key "${PRIVATE_KEY}"

# If you used the HTTP well-known file:
mcp-publisher login http --domain surveysparrow.com --private-key "${PRIVATE_KEY}"
```

## 5. Publish

From the repo root (where `server.json` lives):

```bash
mcp-publisher publish
```

## 6. Verify

```bash
curl "https://registry.modelcontextprotocol.io/v0/servers?search=com.surveysparrow/mcp"
```

## Publishing an update later

1. Bump `version` in `server.json` (semver; each published version must be unique).
2. Re-run `mcp-publisher login ...` if your session expired, then `mcp-publisher publish`.
