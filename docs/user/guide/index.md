# Use the Web UI

English | [中文](index.zh.md)

## Quick Start

Start the Web UI through the [root README](../../../README.md#run); the command prints its URL. This guide begins after that server is running. The `dsh` process uses its invoking directory as the default workspace root.

## Contents

- [Prerequisites](#prerequisites)
- [Configure a Model](#configure-a-model)
- [Choose a Workspace](#choose-a-workspace)
- [Run a Task](#run-a-task)
- [Available Plugins](#available-plugins)
- [Troubleshooting](#troubleshooting)
- [Next Steps](#next-steps)

## Prerequisites

Before proceeding, ensure:
- The Web UI server is running (started via the root README)
- You have a DeepSeek API key from [platform.deepseek.com](https://platform.deepseek.com/)
- You have a project directory ready to work with

## Configure a Model

1. Open **Settings → Models**
2. Enter your [DeepSeek API key](https://platform.deepseek.com/)
3. Click **Save**

The model route becomes usable immediately without restarting the server.

**Learn more:** The [model configuration guide](./providers.md) covers other providers and custom OpenAI-compatible endpoints.

## Choose a Workspace

1. Click **Choose workspace**
2. Click **Add** and navigate to your project directory (where you started `dsh`)
3. Select the folder and confirm

The session composer remains unavailable until a workspace is selected.

## Run a Task

1. Start a new session
2. Send a prompt to the agent. Example:

> Summarize this repository and identify its main packages.

### What the Agent Can Do

The agent can:
- Read and edit workspace files
- Run commands in your project
- Delegate work to plugins
- Maintain and update a task plan

### Permissions

The Web UI will ask before executing operations that require approval under the active permission policy. Review and approve operations as needed.

## Available Plugins

DeepSeek Harness includes a comprehensive plugin system for extending functionality. Plugins are configured in `cordis.yml` and can be loadable (with or without config) or abstract seam packages.

### Plugins with Configuration

#### Web Search - Perplexity
**Package:** `@deepseek-ai/dsh-web-search-perplexity`  
**Requires:** `web`

```typescript
export interface Config {
  /** Perplexity API key. Falls back to $PERPLEXITY_API_KEY. Empty → unavailable. */
  apiKey?: string
  /** Endpoint base; /chat/completions is appended. Defaults to the public API. */
  baseURL?: string
  /** Search model name. Defaults to sonar. */
  model?: string
  /** Upper bound on generated answer tokens. Defaults to 1024. */
  maxTokens?: number
  /** Recency window: day, week, month, year. Omitted = no filter. */
  searchRecency?: 'day' | 'week' | 'month' | 'year'
}
