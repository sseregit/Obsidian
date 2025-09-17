`claude mcp list`
- 설치된 scope의 mcp 리스트

`claude mcp remove {mcp name}`
- mcp 삭제

`claude mcp add complysight-dev -s project -- npx -y @modelcontextprotocol/server-postgres {DBURL}`
- add {mcp의 이름}
- -s scope
	- project
		- project 귀속
	- user
		- 사용자별
	- local
		- 글로벌