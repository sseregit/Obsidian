`~/.claude.json`
- mcp 정보가 있다. 확인할것 scope user

`claude mcp list`
- 설치된 scope의 mcp 리스트

`claude mcp remove {mcp name}`
- mcp 삭제

### postgresql
`claude mcp add complysight-dev -s project -- npx -y @modelcontextprotocol/server-postgres {DBURL}`
- add {mcp의 이름}
- -s scope
	- project
		- project 귀속
	- user
		- 사용자별
	- local
		- 글로벌

### serena
`claude mcp add serena --scope user -- uvx --from git+https://github.com/oraios/serena serena start-mcp-server --context ide-assistant --project "$(pwd)" --enable-web-dashboard false`
- `--enable-web-dashboard false `
	- 대시보드 안뜨게 하는 옵션

### context7
`claude mcp add --transport http context7 https://mcp.context7.com/mcp --header "CONTEXT7_API_KEY: YOUR_API_KEY"`

`claude mcp add --scope user --transport http context7 https://mcp.context7.com/mcp --header "CONTEXT7_API_KEY: $CONTEXT7_API_KEY”`
- 환경변수로 해야함.!

### playwright
`claude mcp add playwright -s user -- npx -y @modelcontextprotocol/server-playwright`
