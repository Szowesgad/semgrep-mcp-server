# MCP Server Semgrep

![MCP Server Semgrep Logo](./logo.svg)

## About the Project

This project was initially inspired by robustness of [Semgrep tool](https://semgrep.dev), [The Replit Team](https://github.com/replit) and their [Agent V2](https://replit.com), as well as the implementation by [stefanskiasan/semgrep-mcp-server](https://github.com/stefanskiasan/semgrep-mcp-server), but has evolved with significant architectural changes for enhanced and easier installation and maintenance.

MCP Server Semgrep is a [Model Context Protocol](https://modelcontextprotocol.io) compliant server that integrates the powerful Semgrep static analysis tool with AI assistants like Anthropic Claude. It enables advanced code analysis, security vulnerability detection, and code quality improvements directly through a conversational interface.

## Benefits of Integration

### For Developers and Development Teams:

- **Holistic Source Code Analysis** - detecting issues throughout the entire project, not just in individual files
- **Proactive Error Detection** - identifying potential problems before they become critical bugs
- **Continuous Code Quality Improvement** - regular scanning and refactoring lead to gradual codebase improvements
- **Stylistic Consistency** - identification and fixing of inconsistencies in code, such as:
  - Arbitrary z-index layers in CSS
  - Inconsistent naming conventions
  - Code duplication
  - "Magic numbers" instead of named constants

### For Security:

- **Automated Code Verification for Known Vulnerabilities** - scanning for known security issue patterns
- **Customized Security Rules** - creating project-specific rules
- **Team Education** - teaching secure programming practices through detection of potential issues

### For Project Maintenance and Development:

- **"Live" Documentation** - AI can explain why a code fragment is problematic and how to fix it
- **Technical Debt Reduction** - systematically detecting and fixing problematic areas
- **Improved Code Reviews** - automatic detection of common issues allows focus on more complex matters

## Key Features

- MCP protocol implementation tailored for Semgrep use cases
- Reduced external dependencies for better long-term maintenance
- Efficient communication protocol focused on Semgrep requirements
- Reorganized project structure and modularization
- Enhanced error handling and security
- Interface and documentation in both English and Polish
- Comprehensive unit tests
- Extensive documentation
- Cross-platform compatibility (Windows, macOS, Linux)
- Flexible Semgrep installation detection
- Compatibility with MCP resources/list and prompts/list methods

## Functions

Semgrep MCP Server provides the following tools:

- **scan_directory**: Scanning source code for potential issues
- **list_rules**: Displaying available rules and languages supported by Semgrep
- **analyze_results**: Detailed analysis of scan results
- **create_rule**: Creating custom Semgrep rules
- **filter_results**: Filtering results by various criteria
- **export_results**: Exporting results in various formats
- **compare_results**: Comparing two sets of results (e.g., before and after changes)

## Common Use Cases

- Code security analysis before deployment
- Detection of common programming errors
- Enforcing coding standards within a team
- Refactoring and improving quality of existing code
- Identifying inconsistencies in styles and code structure (e.g., CSS, component organization)
- Developer education regarding best practices
- Verification of fix correctness (comparing before/after scans)

## Installation

### Prerequisites

- Node.js v18+
- TypeScript (for development)

### Setup

1. Clone the repository:
```bash
git clone https://github.com/Szowesgad/mcp-server-semgrep.git
cd mcp-server-semgrep
```

2. Install dependencies:
```bash
npm install
# or
yarn install
# or
pnpm install
```

> **Note**: The installation process will automatically check for Semgrep availability. If Semgrep is not found, you'll receive instructions on how to install it.

#### Semgrep Installation Options

Semgrep can be installed in several ways:

- **NPM (recommended)**: It's included as an optional dependency
  ```bash
  npm install -g semgrep
  # or
  pnpm add -g semgrep
  ```

- **Python pip**:
  ```bash
  pip install semgrep
  ```

- **Homebrew** (macOS):
  ```bash
  brew install semgrep
  ```

- **Linux**:
  ```bash
  sudo apt-get install semgrep
  # or
  curl -sSL https://install.semgrep.dev | sh
  ```

3. Build the project:
```bash
npm run build
# or
yarn build
# or
pnpm run build
```

## Integration with Claude Desktop

To integrate MCP Server Semgrep with Claude Desktop:

1. Install Claude Desktop
2. Update the Claude Desktop configuration file (`claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "semgrep": {
      "command": "node",
      "args": [
        "/path/to/project/mcp-server-semgrep/build/index.js"
      ]
    }
  }
}
```

3. Launch Claude Desktop and start asking questions about code analysis!

## Usage Examples

### Project Scanning

```
Could you scan my source code in the /projects/my-application directory for potential security issues?
```

### Style Consistency Analysis

```
Analyze the z-index values in the project's CSS files and identify inconsistencies and potential layer conflicts.
```

### Creating a Custom Rule

```
Create a Semgrep rule that detects improper use of input sanitization functions.
```

### Filtering Results

```
Show me only scan results related to SQL injection vulnerabilities.
```

### Identifying Problematic Patterns

```
Find all "magic numbers" in the code and suggest replacing them with named constants.
```

## Creating Custom Rules

You can create custom rules for your project's specific needs. Here are examples of rules you can create:

### Rule to detect inconsistent z-indices:

```yaml
rules:
  - id: inconsistent-z-index
    pattern: z-index: $Z
    message: "Z-index $Z may not comply with the project's layering system"
    languages: [css, scss]
    severity: WARNING
```

### Rule to detect deprecated imports:

```yaml
rules:
  - id: deprecated-import
    pattern: import $X from 'old-library'
    message: "You're using a deprecated library. Consider using 'new-library'"
    languages: [javascript, typescript]
    severity: WARNING
```

## Development

### Testing

```bash
npm test
# or
yarn test
# or
pnpm test
```

### Project Structure

```
├── src/
│   ├── config.ts         # Server configuration
│   ├── index.ts          # Entry point
│   ├── sdk.ts            # MCP protocol interface
│   ├── handlers/         # Request handlers for MCP tools
│   └── utils/            # Utility functions and Semgrep integration
├── scripts/
│   └── check-semgrep.js  # Semgrep detection and installation helper
├── build/                # Compiled JavaScript (after build)
├── test_scan/            # Example files for testing scans
└── tests/                # Unit tests
```

## Further Documentation

Detailed information on using the tool can be found in:
- [USAGE.md](USAGE.md) - Detailed usage instructions
- [README_PL.md](README_PL.md) - Documentation in Polish
- [examples/](examples/) - Example fun and practical Semgrep rules - "The Hall of Code Horrors"

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Developed by

- [Maciej Gad](https://github.com/Szowesgad) - a veterinarian who couldn't find `bash` a half year ago
- [Klaudiusz](https://www.github.com/Gitlaudiusz) - the individual ethereal being, and separate instance of Claude Sonnet 3.5-3.7 by Anthropic living somewhere in the GPU's loops in California, USA

The journey from CLI novice to MCP tool developer

🤖 Developed with the ultimate help of [Claude Code](https://claude.ai/code) and [MCP Tools](https://modelcontextprotocol.io)

## Acknowledgements

- [stefanskiasan](https://github.com/stefanskiasan) for the original inspiration
- [Anthropic](https://www.anthropic.com/) for Claude and the MCP protocol
- [Semgrep](https://semgrep.dev/) for their excellent static analysis tool
