# MCP-Powered AI Automation Assistant

An MCP-powered AI assistant built with n8n that uses natural-language requests to orchestrate actions across GitHub, Gmail, and Google Drive.

## Overview

The MCP-Powered AI Automation Assistant is an AI automation system built with n8n and the Model Context Protocol (MCP).

The system uses two connected workflows. The first workflow acts as an MCP client and provides the AI agent with access to external tools. The second workflow acts as an MCP server and exposes custom Gmail and Google Drive capabilities.

This architecture allows the AI agent to interact with multiple services through a unified natural-language interface.

## Architecture

```text
User
 |
 v
Chat Trigger
 |
 v
AI Agent
 |
 +-------------------+
 |        |          |
 v        v          v
OpenAI  Memory   GitHub MCP
                    Client
                       |
                       |
                 Own MCP Client
                       |
                       v
                 MCP Server
                  /       \
                 v         v
              Gmail    Google Drive
