`~/.codex/config.toml`

### serena
```toml
[mcp_servers.serena]
command = "uvx"
args = ["--from", "git+https://github.com/oraios/serena", "serena", "start-mcp-server", "--context", "codex", "--enable-web-dashboard", "false"]
```

### context7
```toml
[mcp_servers.context7]
args = ["-y", "@upstash/context7-mcp", "--api-key", "$CONTEXT7_API_KEY”]
command = "npx"
startup_timeout_ms = 20000
```
- $CONTEXT7_API_KEY 환경변수 적용 안되니 직접 입력해야함