# WeMush Agent Skills

This repository contains Agent Skills for use with Claude and other AI assistants that support the [Agent Skills specification](https://agentskills.io).

## Available Skills

### wemush-mycology-assistant

Guide mycology research workflows using WeMush's MCP server for specimen tracking, research projects, cultivation analytics, and strain catalog exploration.

**Use when users ask about:**

- Mushroom cultivation and research
- Specimen tracking and management
- Research project participation
- Cultivation analytics and outcomes
- Strain and species information

## Installation

### Claude Code

```bash
# Add as a plugin marketplace (if hosted separately)
/plugin marketplace add wemush/wemush-skills

# Or install directly
/plugin install wemush-mycology-assistant
```

### Claude.ai

Upload the skill folder via Settings > Capabilities > Skills.

### Manual

Copy the skill folder to your skills directory and configure your AI assistant to load it.

## Prerequisites

To use WeMush skills, you need:

1. **WeMush Account**: Sign up at <https://wemush.com>
2. **MCP Server Connection**: Configure the WeMush MCP server in your AI assistant
3. **OAuth Authorization**: Grant appropriate scopes during authentication

## MCP Server Configuration

Add the WeMush MCP server to your Claude configuration:

```json
{
  "mcpServers": {
    "wemush": {
      "url": "https://wemush.com/api/mcp/research/sse",
      "transport": "sse"
    }
  }
}
```

## Documentation

- **Skill Reference**: See `wemush-mycology-assistant/SKILL.md`
- **Tool Documentation**: See `wemush-mycology-assistant/references/REFERENCE.md`
- **WeMush Docs**: <https://wemush.com/docs/claude-connector>

## Support

- Email: <support@wemush.com>
- Documentation: <https://wemush.com/docs/claude-connector>
- Status: <https://wemush.com/status>

## License

Apache-2.0 - See [LICENSE](LICENSE) for details.

## About WeMush

WeMush is a decentralized mycology platform for mushroom cultivation management, specimen tracking, and collaborative research. Learn more at <https://wemush.com>.
