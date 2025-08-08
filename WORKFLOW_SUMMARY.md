# n8n Workflows Summary

This repository contains automation workflows built with [n8n](https://n8n.io/) for managing various communication and scheduling tasks. The workflows are designed to handle job search activities, email automation, WhatsApp interactions, and calendar management.

## Repository Overview

**Purpose**: Save automation workflows as backup in case Docker container is deleted or computer changes are needed.

**Setup Instructions**: 
- Install n8n using Docker: `docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n`
- Import workflows by dragging and dropping JSON files into the n8n interface
- Configure required credentials (Gmail, Google Sheets, OpenAI, etc.)

## Workflow Categories

### 📧 Gmail Workflows

#### 1. **Email Job Application Tracker** (`gmail/app-to-sheet.json`)
- **Purpose**: Automatically tracks job application confirmations and logs them to Google Sheets
- **Trigger**: Gmail trigger (every minute) for new emails
- **Process**: 
  - Classifies emails using OpenAI LLM to identify job application receipts
  - Extracts company names from email content
  - Updates Google Sheets with weekly tracking data
- **Key Features**: Filters out rejection emails, spam, and EEO forms

#### 2. **Gmail Spam Cleaner** (`gmail/clear-spam.json`)
- **Purpose**: Automatically deletes unwanted emails from specific senders
- **Trigger**: Scheduled every 2 hours
- **Process**: Filters emails from job alert services and deletes them in batches
- **Targeted Senders**: tecnoempleo, jobright.ai, jobleads.com, heartbeat.chat, LinkedIn job alerts

#### 3. **Gmail Appointment Scheduler** (`gmail/email-starter.json`, `gmail/gmail-apt.json`)
- **Purpose**: AI-powered email scheduling assistant
- **Trigger**: Gmail trigger for unread emails
- **Process**:
  - Classifies incoming emails to detect appointment requests
  - Uses OpenAI Agent with Google Calendar integration
  - Automatically composes and sends scheduling responses
  - Marks emails as read after processing
- **Features**: Calendar availability checking, 15-minute buffer management, Calendly link inclusion

### 💬 Chat & Communication Workflows

#### 4. **LinkedIn/Gmail Message Processor** (`chat/linkedin-gmail-apt.json`)
- **Purpose**: Processes recruiter messages for appointment scheduling
- **Trigger**: Chat message trigger
- **Process**:
  - Extracts sender details (name, company, job title)
  - Integrates with Google Calendar for availability
  - Generates personalized responses using AI agent
- **Key Features**: Context-aware scheduling, professional response generation

#### 5. **MCP Integration Example** (`chat/mcp-example.json`)
- **Purpose**: Demonstrates Model Context Protocol (MCP) integration with AI agents
- **Features**: 
  - Multiple tool functions (text case conversion, random data generation, joke retrieval)
  - Google Calendar MCP server integration
  - Memory management for conversation context
- **Tools Available**: Calendar management, text processing, data generation

### 📱 WhatsApp Workflows

#### 6. **Knowledge Base Agent** (`whatsapp/knowledge-agent.json`)
- **Purpose**: AI-powered customer support bot with document processing capabilities
- **Trigger**: WhatsApp message trigger
- **Process**:
  - Handles multiple message types (text, audio, image, documents)
  - Uses MongoDB vector search for knowledge retrieval
  - Processes various file formats (PDF, Excel, CSV, etc.)
  - Maintains conversation memory per user
- **Key Features**: Multi-modal input processing, vector search, document analysis

#### 7. **Sales Agent** (`whatsapp/sales-agent.json`)
- **Purpose**: WhatsApp sales chatbot with product catalog integration
- **Trigger**: WhatsApp message trigger
- **Process**:
  - Downloads and processes product brochures (PDF)
  - Creates vector store from product documentation
  - Provides product information and sales support
  - Filters non-text messages with appropriate responses
- **Features**: Product catalog search, sales-focused conversations, automated responses

## Technical Components

### AI & LLM Integration
- **OpenAI Models**: GPT-4o, GPT-4o-mini for different complexity needs
- **Use Cases**: Text classification, information extraction, conversation agents
- **Features**: System message prompts, context management, tool integration

### Vector Stores & Knowledge Management
- **MongoDB Atlas**: Vector search for large-scale knowledge bases
- **In-Memory Vector Store**: For simpler use cases and development
- **Document Processing**: PDF, Excel, CSV, and various text format support
- **Embeddings**: OpenAI text-embedding models for semantic search

### External Integrations
- **Google Services**: Gmail, Google Calendar, Google Sheets, Google Docs
- **Communication Platforms**: WhatsApp Business API
- **Authentication**: OAuth2 for secure API access
- **File Processing**: Multi-format document extraction and analysis

### Automation Features
- **Scheduled Triggers**: Time-based automation for periodic tasks
- **Event-Driven**: Email and message triggers for real-time responses
- **Error Handling**: Fallback mechanisms and user notifications
- **Memory Management**: Conversation context and user session tracking

## Files Overview

| File | Category | Purpose |
|------|----------|---------|
| `README.md` | Documentation | Setup instructions and repository overview |
| `html_body.html` | Unknown | Encoded HTML content (appears to be CTF-related) |
| `gmail/app-to-sheet.json` | Gmail | Job application tracking |
| `gmail/clear-spam.json` | Gmail | Automated spam cleanup |
| `gmail/email-starter.json` | Gmail | Email scheduling assistant |
| `gmail/gmail-apt.json` | Gmail | Advanced appointment scheduling |
| `chat/linkedin-gmail-apt.json` | Chat | Recruiter message processing |
| `chat/mcp-example.json` | Chat | MCP integration demo |
| `whatsapp/knowledge-agent.json` | WhatsApp | AI customer support |
| `whatsapp/sales-agent.json` | WhatsApp | Sales chatbot |

## Security & Best Practices

- **Credential Management**: Uses n8n's secure credential storage system
- **API Security**: OAuth2 authentication for Google services
- **Data Sanitization**: Reminder to sanitize JSON files of internal IDs
- **Error Handling**: Appropriate fallbacks for unsupported operations
- **Rate Limiting**: Scheduled intervals to prevent API overuse

## Setup Requirements

### Required Credentials
- OpenAI API key
- Google OAuth2 credentials (Gmail, Calendar, Sheets)
- WhatsApp Business API access
- MongoDB Atlas connection (for vector search workflows)

### System Dependencies
- Docker with n8n container
- Persistent volume for data storage
- Network access for webhook endpoints
- SSL certificates for production webhooks

This collection of workflows demonstrates advanced automation capabilities combining AI, communication platforms, and productivity tools to streamline job search, customer service, and business communication processes.