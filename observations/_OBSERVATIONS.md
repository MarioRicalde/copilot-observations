# OBSERVATIONS

This document contains observations and notes related to the project. It serves as a reference for key insights, challenges faced, and lessons learned.

## Important intentional traps implemented for the models to fall into:

These 2 steps causes less-than-state-of-the-art models to ommit the table style in the final output.

- Table is generated on agent step #4.
- On step #5 we decorate part of the string.

## 12/20/2025

### Case: Handing off between agents with different tool access

Using Grok Code Fast 1 (0x).

If you don't limit the tools available to the model, it tends to read the content of all agents and do unnecessary things. Making the operation take longer and produce less relevant outputs.

![alt text](handoff-with-all-tools.png)

![alt text](handoff-just-agent-tool.png)

### Case: `copilot-handoffs-subagent-number-processor` instead of proper handoff

Using Grok Code Fast 1 (0x).

When not using specifying `handoff` properly, and instead we use:

```prompt
#tool:agent/runSubagent number-converter-second
```

The model seems to properly follow the instructions and use the subagents to properly follow the chain of agents required to produce the output; however, the output is less relevant and less accurate than when using proper handoff.

![alt text](handoff-via-subagents.png)

In pracftice it tends to fail quite a bit in producing the correct final output; however, it's possible that updating the agents to include some of the context that was lost from the handoff prompt will help.
