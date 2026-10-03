# How to use coding agents (Andrew Ng)

- [How to use coding agents by Andrew Ng](https://www.deeplearning.ai/the-batch/the-ai-engineering-skills-map-in-detail-using-coding-agents)
- Andrew Ng says:

>“I find that social media often gives oversimplified descriptions of how to use coding agents. For example, it is sometimes useful to get agents to run autonomously for hours and burn millions or tens of millions of tokens. But currently the practical utility of very long-horizon tasks — especially relative to their cost — has been amplified beyond reality. Instead, most effective coding agent use is a complex, highly iterative process, and being able to intervene with high-skill judgement gives much better results.”

- the human _directs_ and _supervises_ the work and go back and forth and frequently supervise
- _manage_ the context
- for example in the context of [Math AI](https://neelsoumya.github.io/science_blog_fun/irodov_figure1.html). See examples from Knuth and Riemann hypothesis. 
- automated testing and evals?
- code review by agents. update `agents.md` and `claude.md` with information on repository and assumptions
- see [vibesafe](https://github.com/lawrennd/vibesafe)
- manage contexts across agents across different developers 
- [🎥 video: agentic development using NVIDIA Jetson](https://www.youtube.com/watch?v=OF_ryVZmB3w)


The key steps are:
- Planning
- Execution
- Deployment and monitoring

>This high-level workflow is similar to the one typically used to build software before coding agents. Now, we focus much less on code and instead focus on deciding what to build, designing the architecture, writing the spec, and verifying outputs.

To use coding agents effectively in this workflow, the key skills are:

- Directing the workflow
- Enabling agent autonomy
- Reviewing the work
- Customizing the agent and its environment
- Coding agent foundations

>Directing the workflow. You know how to navigate each step of the workflow above. This involves deciding how much human and how much agent effort to spend on each and when to go back to an earlier step to iterate. It requires deeply understanding the tradeoffs of speed, cost, technical risk, and human effort, so you can decide how much to research and plan up front, when to retain human ownership over critical work, how to choose the architecture, how much detail to write into a set of planning artifacts (like a spec), and how to decompose the work into verifiable steps.

>Enabling agent autonomy. When applying a coding agent to the steps in the workflow, you choose the autonomy level: Do you watch it and go back-and-forth interactively or delegate a larger chunk of work to it? And when do you set a clear goal and have it loop until it succeeds? Additionally, you have to manage the context carefully for the agent. As the build proceeds through different phases, you will calibrate when to make sure key learnings, user feedback, and assumptions — including assumptions that changed partway through the build — are captured for the agent to use downstream. Additionally, you will decide when to set up many agents to run in parallel on a decomposition of the task — either by having a human or a higher-level agent orchestrate these other agents — and how to manage human attention across concurrent agent sessions. You also know how to run agents safely, setting permissions and gating actions appropriately to let development proceed quickly while limiting the risk of leaks, data loss, or other damage.

>Reviewing the work. The output of a coding agent is uncertain. We don’t know in advance what good ideas it might come up with and what bugs it will implement. Reviewing and verifying the output is a key step to ensure you are getting the result you want and to redirect the agent if not. You will design testing and validation that is matched to the task, applying both behavioral and functional verification as needed. You might also test user flows, perhaps having an agent provide screenshots as evidence of success or failure. For qualitative/behavioral evaluation, eval sets, perhaps with LLM-as-a-judge, can be used.

>Customizing the agent and its environment. Your ability to update both the agent and the environment it works in allows your agents to efficiently get the context they need, access tools, and build correctly and efficiently. You know how to integrate agent skills, plugins, and MCP servers. Occasionally you will prune them when they are no longer necessary (such as when a new model obviates an old skill). You can use hooks to automate repeatable parts of the development process, like triggering automated code reviews or CI/CD pipelines. You can also maintain the environment the agent works in: updating the standing context (such as AGENTS.md or CLAUDE.md) with information on the codebase, key architectural assumptions, code style, and data access patterns. You know how to preserve state across multiple sessions and across parallel agents, and accumulate agent learnings over time, perhaps by running post-run retrospectives to capture what did and did not work. You also know how to set up consistent conventions and structure to make your codebase navigable to the agent, and how to occasionally clear out agent-generated debt. When you work in a team, you consider how to coordinate context across different developers’ agents.

>Coding agent foundations. Finally, to make good decisions throughout, you have a good understanding of how coding agents work: how they carry out codebase search/retrieval, how they manage their context windows, how different operations (like adding tool calls, MCP servers, etc.) affect context, how agents and subagents interact, and how the agent is built by wrapping a harness around an LLM. This makes the agent less of a black box and helps you to recognize failure modes, such as overengineering a simple solution, losing rigor because the agent lacks an explicit verification process, stopping short of the goal, or agent actions that risk destruction of files or production data. It also helps you reason about the agent’s state and steer it by giving it the right prescription or context. And when monitoring a run, this understanding allows you to better spot when the agent goes off-track and requires your intervention.


- [Humour video: vibe coding cleanup specialist](https://www.youtube.com/shorts/_10OigKn0Pc)

![image](images/vibe_coding_humour.jpeg)

- Agentic Coding is powerful, but someone still has to clean up after the "Large Mess Maker" (LMM)! 🧹 Our specialist uses an innovative (feather duster) method to refactor chaotic spaghetti into clean, optimized output. Just another day in the Agentic Cleanup Protocol. Who needs a digital deep clean? 💻🤖

