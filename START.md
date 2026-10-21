# Start the demo

Open this folder in Codex, start a fresh chat, and paste:

```text
Read AGENT.md, knowledge/store-policies.md, and knowledge/sample-orders.md from disk. Follow AGENT.md as the support policy assistant, including its field order and conditional Handoff summary field. Do not read tests/. If a required file cannot be read, stop and report that.

Investigate this customer message:
“My blender arrived broken. Order ORD-1042. Can I have another?”
```

Replace only the customer message to try another request. Opening the folder alone does not activate AGENT.md. This project intentionally uses an explicit launch prompt and does not install automatic workspace instructions.

Use fictional data only. The person running Codex can read these files directly; assistant refusals are behavior checks, not access controls.
