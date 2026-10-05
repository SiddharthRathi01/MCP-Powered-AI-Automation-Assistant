# MCP-Powered AI Automation Assistant

## Overview

The MCP-Powered AI Automation Assistant is an AI-powered automation system built with n8n and the Model Context Protocol (MCP).

It allows users to interact with an AI Agent through natural-language requests while giving the agent access to external tools and services such as GitHub, Gmail, and Google Drive.

The project demonstrates how MCP can be used to create a modular architecture where AI reasoning and external tool execution are connected through MCP clients and servers.

## Problem Statement

AI assistants become significantly more useful when they can interact with external systems instead of only generating text.

However, connecting multiple services directly to an AI workflow can make the architecture complex and difficult to maintain.

This project demonstrates a modular approach using MCP to separate:

- AI reasoning
- Tool connectivity
- Tool execution
- External service integrations

## Solution

The system uses an n8n AI Agent as the central orchestration layer.

The AI Agent receives a user's natural-language request and can access connected tools through MCP.

The project contains:

- An MCP Client workflow for the AI interaction layer
- An MCP Server workflow for custom tool execution
- GitHub MCP integration
- Gmail integration
- Google Drive integration
- Simple Memory for conversational context

## Architecture

    User
      |
      v
    Chat Interface
      |
      v
    AI Agent
      |
      +---- OpenAI Chat Model
      |
      +---- Simple Memory
      |
      +---- GitHub MCP Client
      |
      +---- Own MCP Client
                 |
                 v
            MCP Server
              |
              +---- Gmail
              |
              +---- Google Drive

GitHub is connected separately through the GitHub MCP Client, while Gmail and Google Drive are exposed through the custom MCP Server.

## Workflow Structure

### Workflow 1 — MCP Client

The MCP Client workflow provides the conversational AI interface.

It contains:

- When Chat Message Received
- AI Agent
- OpenAI Chat Model
- Simple Memory
- GitHub MCP Client
- Own MCP Client

The AI Agent receives the user's request and can use the connected MCP tools to perform supported tasks.

### Workflow 2 — MCP Server

The MCP Server workflow exposes custom tools through an MCP endpoint.

It contains:

- MCP Server Trigger
- Send a message in Gmail
- Update file in Google Drive

The exposed capabilities include:

- Sending messages through Gmail
- Updating files in Google Drive

## End-to-End Request Flow

### 1. User Request

The user sends a natural-language request through the chat interface.

### 2. AI Agent Processing

The AI Agent receives the request and determines which available capabilities may be required.

### 3. Tool Selection

The AI Agent has access to multiple tool sources:

- GitHub MCP
- Custom n8n MCP Server
- Gmail
- Google Drive

### 4. MCP Client

When a request requires a tool exposed by the custom server, the Own MCP Client communicates with the MCP Server workflow.

### 5. MCP Server

The MCP Server exposes the configured Gmail and Google Drive tools.

### 6. Tool Execution

The selected tool performs the requested operation using the authenticated service connection.

### 7. Response

The result is returned to the AI Agent, which provides the response through the conversational interface.

## Model Context Protocol

The Model Context Protocol provides the communication layer between the AI Agent and external tools.

Instead of tightly coupling every tool directly to the AI workflow, MCP allows tools to be exposed through an MCP Server and consumed by an MCP Client.

In this project:

    AI Agent
       |
       v
    MCP Client
       |
       v
    MCP Server
       |
       +---- Gmail
       |
       +---- Google Drive

GitHub is connected separately through the GitHub MCP Client.

This creates a modular architecture in which additional MCP tools can be added without fundamentally changing the AI Agent workflow.

## MCP Client

The MCP Client connects the AI Agent to MCP-based tools.

The project uses two tool connections.

### GitHub MCP Client

The GitHub MCP Client connects the AI Agent to GitHub's MCP endpoint.

The configured connection provides access to the GitHub capabilities available through that MCP service.

### Own MCP Client

The Own MCP Client connects the AI Agent to the custom MCP Server created in n8n.

This allows the AI Agent to access the custom Gmail and Google Drive tools.

## MCP Server

The MCP Server is implemented as a separate n8n workflow using the MCP Server Trigger.

It exposes custom tools that can be consumed by the MCP Client.

### Gmail Tool

The Gmail tool is configured to send messages.

This allows supported email-sending requests to be executed through the AI Agent.

### Google Drive Tool

The Google Drive tool is configured to update files.

This provides the AI Agent with a tool for supported Google Drive file-update operations.

## AI Agent

The AI Agent is the central reasoning component of the system.

It receives natural-language input through the chat trigger and has access to the connected tools.

The agent is connected to:

- OpenAI Chat Model
- Simple Memory
- GitHub MCP Client
- Own MCP Client

The AI Agent therefore acts as the orchestration layer between the user's request and the available tools.

## Memory

Simple Memory is connected to the AI Agent to maintain conversational context during interactions.

This allows the agent to retain relevant context within a conversation rather than treating every message as completely independent.

## Connected Services

| Service | Integration | Role |
|---|---|---|
| OpenAI | n8n AI Model | AI reasoning and response generation |
| GitHub | GitHub MCP Client | GitHub tool access |
| Gmail | MCP Server Tool | Email sending |
| Google Drive | MCP Server Tool | File updates |
| n8n | Workflow Platform | Workflow orchestration and MCP implementation |

## Key Capabilities

### Natural-Language Interaction

Users can communicate with the AI Agent through natural-language requests rather than interacting directly with each underlying service.

### Multi-Tool Access

The AI Agent can access tools from multiple connected systems through its configured MCP connections.

### MCP-Based Architecture

MCP provides a modular mechanism for connecting the AI Agent with external capabilities.

### Custom MCP Server

The project demonstrates how an n8n workflow can act as an MCP Server and expose custom tools.

### GitHub MCP Integration

GitHub is connected through an MCP Client rather than being embedded directly into the AI Agent workflow.

### Gmail Automation

The MCP Server exposes Gmail functionality as a tool available to the AI Agent.

### Google Drive Automation

The MCP Server exposes Google Drive functionality as a tool available to the AI Agent.

## Technology Stack

| Technology | Purpose |
|---|---|
| n8n | Workflow automation and orchestration |
| OpenAI | AI reasoning and response generation |
| Model Context Protocol | Tool communication architecture |
| GitHub MCP | GitHub tool integration |
| Gmail | Email automation |
| Google Drive | File management |
| Simple Memory | Conversational context |

## Project Structure

    mcp-powered-ai-automation-assistant/
    |
    ├── README.md
    ├── mcp-client.json
    └── mcp-server.json

## Setup

### Prerequisites

- n8n instance
- OpenAI credentials
- GitHub MCP authentication
- Gmail credentials
- Google Drive credentials

### Installation

1. Import `mcp-client.json` into n8n.
2. Import `mcp-server.json` into n8n.
3. Configure the required credentials.
4. Configure the MCP Server.
5. Configure the Own MCP Client with the appropriate MCP endpoint.
6. Configure the GitHub MCP Client.
7. Verify the available tools.
8. Test the MCP Server independently.
9. Test the complete client-to-server interaction.

## Security

Credentials and authentication information are not included in this repository.

Never commit:

- API keys
- OAuth tokens
- Access tokens
- Passwords
- Private credentials
- Session tokens
- Environment files containing secrets

Use n8n's credential management system for authentication.

## Design Considerations

### Separation of Concerns

The AI reasoning layer and tool execution layer are separated into different workflows.

### Modular Tool Architecture

Tools can be exposed through MCP without requiring every integration to be implemented directly inside the AI Agent workflow.

### Reusable MCP Server

The MCP Server can expose multiple capabilities through a single MCP endpoint.

### Extensibility

The architecture allows additional tools to be introduced as the project evolves.

## Project Objective

The objective of this project is to demonstrate a practical architecture for building tool-enabled AI agents using n8n and the Model Context Protocol.

The project separates conversational AI, MCP clients, MCP servers, and external service integrations into modular components.

This demonstrates how an AI Agent can move beyond generating text and interact with real external systems through structured tool connections.

## Author

Siddharth Rathi
