# Vapi MCP Server Containerized in Docker MCP Gateway

## 1) Build a proxy MCP server image
Create a Dockerfile:

```Dockerfile
FROM node:20-alpine
RUN npm i -g mcp-remote
ENV VAPI_TOKEN=""
ENTRYPOINT ["sh","-c","mcp-remote https://mcp.vapi.ai/mcp --header \"Authorization: Bearer ${VAPI_TOKEN}\""]
```

Build it:

```bash
docker build -t vapi-mcp-proxy:latest .
```

## 2) Create a custom MCP catalog entry
Example `vapi-catalog.yaml`:

```yaml
name: vapi-catalog
displayName: Vapi Catalog
registry:
  vapi-mcp:
    title: "Vapi MCP Proxy"
    description: "Proxy to Vapi hosted MCP server"
    type: "server"
    image: "vapi-mcp-proxy:latest"
    secrets:
      - name: "vapi-mcp.token"
        env: "VAPI_TOKEN"
        example: "YOUR_VAPI_API_KEY"
```

## 3) Store your Vapi API key in Docker MCP secrets

```bash
docker mcp secret set vapi-mcp.token=YOUR_VAPI_API_KEY
```

## 4) Run the MCP Gateway with your catalog

```bash
docker mcp gateway run --catalog ./vapi-catalog.yaml --servers vapi-mcp
```

## 5) Connect your MCP client to the Gateway
Use your MCP client’s normal “connect to gateway” configuration.

- For Docker’s MCP Toolkit: `docker mcp client connect <client>`

## Notes
- Vapi’s hosted MCP endpoint: `https://mcp.vapi.ai/mcp`
- Proxy uses `mcp-remote` to forward MCP traffic with the `Authorization: Bearer` header.
