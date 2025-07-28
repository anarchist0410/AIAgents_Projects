# AI ASSISTANT -MCP Agent Interactive Chat

A sophisticated conversational AI system that leverages the Model Context Protocol (MCP) to provide intelligent interactions with web browsing, search, and accommodation booking capabilities.

## Overview

This application implements an interactive chat interface powered by Qwen 3 32B model through Groq API, enhanced with MCP (Model Context Protocol) servers for extended functionality. The system features persistent conversation memory, multi-step reasoning, and integration with multiple external services.

## Features

### Core Capabilities
- **Conversational Memory**: Maintains context across multiple exchanges for coherent, contextual responses
- **Multi-Step Reasoning**: Executes complex workflows with up to 15 reasoning steps
- **Interactive Command Interface**: Simple command-line interface with intuitive controls
- **Graceful Error Handling**: Robust error management for reliable operation

### MCP Server Integrations
- **Web Automation** (`@playwright/mcp`): Advanced web browsing, form filling, and page interaction capabilities
- **Accommodation Search** (`@openbnb/mcp-server-airbnb`): Real-time Airbnb property search and analysis
- **Web Search** (`duckduckgo-mcp-server`): Privacy-focused web search functionality

## Prerequisites

### System Requirements
- Python 3.8+
- Node.js 14+ (for MCP servers)
- Internet connection for API access

### API Keys
- **Groq API Key**: Required for LLM access
  - Obtain from [Groq Console](https://console.groq.com/)
  - Supports Qwen 3 32B model

## Installation

### 1. Clone Repository
```bash
git clone <repository-url>
cd mcp-agent-chat
```

### 2. Python Dependencies
```bash
pip install -r requirements.txt
```

Required packages:
```
python-dotenv
langchain-groq
mcp-use
asyncio
```

### 3. Environment Configuration
Create a `.env` file in the project root:
```env
GROQ_API_KEY=your_groq_api_key_here
```

### 4. MCP Server Setup
The application automatically initializes MCP servers via npx. Ensure Node.js is installed and accessible.

## Configuration

### MCP Servers Configuration (`browser_mcp.json`)
```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@playwright/mcp@latest"]
    },
    "airbnb": {
      "command": "npx", 
      "args": ["-y", "@openbnb/mcp-server-airbnb"]
    },
    "ddg-search": {
      "command": "npx",
      "args": ["-y", "duckduckgo-mcp-server"]
    }
  }
}
```

### Agent Parameters
- **Model**: `qwen/qwen3-32b` via Groq
- **Max Steps**: 15 (configurable)
- **Memory**: Enabled by default
- **Config File**: `browser_mcp.json`

## Usage

### Starting the Application
```bash
python main.py
```

### Interactive Commands
- **Chat**: Simply type your message and press Enter
- **Exit**: Type `exit` or `quit` to end the session
- **Clear History**: Type `clear` to reset conversation memory

### Example Interactions

#### Web Browsing
```
You: Navigate to example.com and tell me about the main content
Assistant: I'll browse to example.com and analyze the content for you...
```

#### Accommodation Search
```
You: Find 3-bedroom apartments in Paris for next month under €200/night
Assistant: I'll search for 3-bedroom accommodations in Paris within your budget...
```

#### Web Search
```
You: Search for recent developments in quantum computing
Assistant: I'll search for the latest quantum computing news and developments...
```

## Architecture

### Core Components
- **MCPAgent**: Orchestrates LLM interactions with MCP servers
- **MCPClient**: Manages connections to external MCP servers
- **ChatGroq**: Interfaces with Groq API for LLM access
- **Memory System**: Maintains conversation context and history

### Data Flow
```
User Input → MCPAgent → LLM Processing → MCP Server Interaction → Response Generation
```

### Error Handling
- Automatic retry mechanisms for API failures
- Graceful degradation when MCP servers are unavailable
- Comprehensive error logging and user feedback

## Customization

### Adding New MCP Servers
1. Update `browser_mcp.json` with new server configuration
2. Ensure the MCP server package is available via npx
3. Restart the application

### Modifying Agent Behavior
- **Max Steps**: Adjust `max_steps` parameter in `MCPAgent` initialization
- **Model Selection**: Change the model parameter in `ChatGroq` initialization
- **Memory Settings**: Toggle `memory_enabled` for different conversation modes

## Troubleshooting

### Common Issues

#### API Key Errors
- Verify `.env` file exists and contains valid `GROQ_API_KEY`
- Check API key permissions and quota

#### MCP Server Connection Issues
- Ensure Node.js is installed and accessible
- Verify internet connection for package downloads
- Check firewall settings for outbound connections

#### Performance Issues
- Monitor API rate limits
- Consider reducing `max_steps` for simpler interactions
- Clear conversation history periodically with `clear` command

## Security Considerations

- **API Keys**: Never commit `.env` files to version control
- **Input Validation**: The system includes built-in input sanitization
- **Network Security**: All external communications use secure protocols
- **Data Privacy**: Conversation history is stored locally and not transmitted

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/enhancement`)
3. Commit changes (`git commit -am 'Add new feature'`)
4. Push to branch (`git push origin feature/enhancement`)
5. Create Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For issues and questions:
- Check the troubleshooting section above
- Review MCP server documentation
- Submit issues via the repository issue tracker

## Acknowledgments

- **MCP Protocol**: Model Context Protocol for extensible AI interactions
- **Groq**: High-performance LLM inference
- **Qwen Model**: Advanced language understanding capabilities
- **Community**: MCP server developers and maintainers
