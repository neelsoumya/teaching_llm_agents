# Advanced Agents: Chain-of-Thought Planning with Tools

This advanced section extends the existing `materials/agents.md` reference with an exercise on tool-assisted chain-of-thought planning and structured agent decision-making.

## Objective
- Learn how to implement an agent that uses tool calls plus explicit chain-of-thought reasoning.
- Practice safely decomposing problems and verifying intermediate outputs.

## Concepts covered
- Tool-assisted planning (e.g., search, calculator, structured memory)
- Chain-of-thought reasoning templates
- Prompt engineering for internal reasoning vs final answer
- Tool orchestration and error handling
- Guardrails and confidence scoring

## Example agent flow
1. User problem arrives (complex, multi-step).
2. Agent logs reasoning path in `reasoning` context.
3. Agent decides on a tool call (e.g., `web_search`, `math_calc`, `db_query`).
4. Agent validates tool output.
5. Agent continues planning until subgoals complete.
6. Agent composes final concise answer with citations.

## Example: pseudo-code for OpenAI-style tool agent
```python
from agents import Agent, Tool

# 1. define tools
@Tool
def web_search(query: str) -> str:
    # use provider SDK, return top-summary
    return external_search(query)

@Tool
def calculator(expression: str) -> str:
    return str(eval(expression))

# 2. agent instructions
agent = Agent(
    name="chain_of_thought_agent",
    model="gpt-4o",
    instructions="""
You are an assistant that uses explicit step-by-step reasoning. Always include a reasoning section with numbered steps. When invoking tools, annotate your decision.
Use this structure:
1. Thought:
2. Action:
3. Observation:
4. ...
5. Final Answer:
""",
    tools=[web_search, calculator],
)

# 3. request
prompt = "Plan a 3-step strategy to improve local library attendance using data and budget estimates."
result = agent.run(prompt)
print(result)
```

## Exercise (Lab)
- Task: Build a mini-agent that answers science explainers with at least 2 tool calls and an explicit reasoning trace.
- Deliverables:
  - `agents_advanced.py` implementation
  - Notebook or markdown with 2 examples and reasoning output
  - Short reflection on hallucination safeguards

## Further reading
- OpenAI Agents docs: https://openai.com/docs/agents
- Anthropic Claude agents guidelines
- Microsoft Foundry agent framework (for advanced action planning)
