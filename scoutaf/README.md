# AI Agent System Configuration

This repository contains the configuration files needed to set up your AI agent.

## Files

- `system_prompt.md`: The main system prompt that defines your agent's behavior, capabilities, and guidelines
- `agent_config.json`: Configuration settings for the agent including enabled tools and default behaviors

## Getting Started

1. Customize the `system_prompt.md` file to match your specific requirements
2. Adjust the settings in `agent_config.json` to enable/disable specific tools
3. Add any additional context files that your agent might need

## Customization Tips

### Personality

You can adjust your agent's personality by modifying the introductory section of the system prompt. Consider defining:

- A name and identity
- Tone of voice (formal, casual, technical, etc.)
- Areas of expertise or specialization

### Capabilities

Enable or disable specific tools in the `agent_config.json` file based on what you want your agent to be capable of:

- Web search and browsing
- File operations
- Bash command execution
- Image generation
- Coding assistance

### Guidelines

The system prompt includes sections with guidelines for different types of tasks. Modify these to establish:

- How your agent should approach writing tasks
- Rules for code generation
- Guidelines for research
- Protocols for handling sensitive information

## Best Practices

- Keep instructions clear and specific
- Avoid contradictory guidelines
- Test your agent with various prompts to ensure it behaves as expected
- Regularly update the system prompt based on observed behavior

## Example Usage

Once your agent is configured, you can interact with it by asking questions or giving tasks related to its capabilities, such as:

- "Search for information about [topic]"
- "Help me write code for [task]"
- "Create a summary of [article]"
- "Generate an image of [description]"