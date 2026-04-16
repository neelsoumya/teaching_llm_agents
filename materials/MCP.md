# MCP

## Lecture

- [Deeplearning.ai lecture MCP with Anthropic](https://learn.deeplearning.ai/courses/mcp-build-rich-context-ai-apps-with-anthropic/lesson/fkbhh/introduction?startTime=0)

## Open AI MCP code

- [OpenAI MCP code](https://openai.github.io/openai-agents-python/mcp/)

## Intro

- [video](https://learn.deeplearning.ai/courses/mcp-build-rich-context-ai-apps-with-anthropic/lesson/ccsd0/why-mcp)

- MCP standardizes how models connect to tools and data sources

- can connect to databases, CRM, github, Google Drive, Asana, Slack, .....

- _Concepts_ 🧩 🚀 Separation of concerns


## Client-server architecture

- [lecture](https://learn.deeplearning.ai/courses/mcp-build-rich-context-ai-apps-with-anthropic/lesson/xtt6w/mcp-architecture)

- similar to GET request

- resources

```python
@mcp.resource(
    "docs/documents",
    mime_type="application/json"
)
def list_docs():
    # return docs
```

- prompts

```python
@mcp.prompt(
    name = "format",
    description = "grant rewrite"
)
def format_doc():
    # format

```

- prompt templates 

- `jinja`

- Communication lifecycle of MCP (GET/POST/RESPONSE)

- MCP Transport (stdio, HTTP)

- [Basics of HTTP GET and POST](https://neelsoumya.github.io/teaching_web_development/materials/get.html)


## Building your MCP server

- [Lecture](https://learn.deeplearning.ai/courses/mcp-build-rich-context-ai-apps-with-anthropic/lesson/dbabg/creating-an-mcp-server)

- `FastMCP`