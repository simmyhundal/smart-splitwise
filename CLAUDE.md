# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

A collection of n8n workflow automations built for a LinkedIn course on AI workflow automation. Workflows are created and managed via the n8n MCP server; finished workflow definitions are exported as JSON and committed to this repo.

## n8n Setup

- n8n runs locally at `http://localhost:5678`
- Interact with n8n via MCP tools (not the web UI) when working in Claude Code
- MCP tools available: `n8n_create_workflow`, `n8n_list_workflows`, `n8n_get_workflow`, `n8n_update_full_workflow`, `n8n_test_workflow`, `n8n_deploy_template`, etc.

## Conventions

- **LLM preference**: Default to Anthropic/Claude models (`claude-sonnet-4-6`, `claude-opus-4-8`) over OpenAI when the model is configurable in a workflow.
- **Export workflows**: After creating or updating a workflow, export its JSON definition and save it to `workflows/<workflow-name>.json` in this repo.
- **Test before done**: Run `n8n_test_workflow` to validate a workflow executes successfully before marking any task complete.
- **Workflow JSON**: Keep exported workflow JSON files human-readable — do not minify.
