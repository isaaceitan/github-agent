# github-agent

This repository is for experimenting with assistants and automation that talk to **GitHub** through tools exposed via the **Model Context Protocol (MCP)**.

## What is the Model Context Protocol (MCP)?

**MCP** is an open protocol that lets applications (such as IDEs and AI assistants) connect to external data and actions in a **standard, structured way**. Instead of each product inventing its own plugin API, MCP defines how a *host* discovers and calls capabilities provided by an MCP *server*.

Think of it as **USB for AI tools**: one protocol, many backends (GitHub, databases, browsers, internal APIs), with clear contracts for what can be invoked and what data can be read.

## Core ideas

| Concept | Role |
|--------|------|
| **Host** | The client application (e.g. an editor or agent runtime) that runs the model and connects to MCP servers. |
| **MCP server** | A process or service that exposes **tools**, **resources**, and sometimes **prompts** to the host. |
| **Tools** | Callable actions (e.g. “create issue”, “search code”) with typed parameters and results. |
| **Resources** | Addressable content the model can fetch (files, docs, URIs) often with MIME types. |
| **Prompts** | Optional reusable prompt templates registered by the server. |

The host negotiates capabilities with each server so the model only uses operations the server actually supports.

## Why it matters for a “GitHub agent”

- **Safety and clarity**: Tools are explicit; the assistant does not get arbitrary shell on your machine unless you expose that as a tool.
- **Composability**: You can combine a GitHub MCP server with others (browser, docs, ticketing) in one workspace.
- **Governance**: Access is mediated by authentication and scopes on the GitHub side, separate from the model.

## Typical transport

MCP servers are often reached over **stdio** (local process) or **HTTP** (remote), depending on the host. The wire format and lifecycle are defined by the protocol so different hosts can interoperate with the same server implementation.

## Learn more

- Official overview and specification: search for **Model Context Protocol** on [modelcontextprotocol.io](https://modelcontextprotocol.io) (Anthropic’s MCP documentation).

---

*Repository description: experimenting with MCP-driven workflows against GitHub.*
