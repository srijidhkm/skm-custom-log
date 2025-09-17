# Custom Log Highlighter

A Visual Studio Code extension that provides customizable syntax highlighting for `.log` files, designed to enhance readability for log files with custom formats. It highlights timestamps, log levels (e.g., ERROR, INFO, DEBUG), and messages with color-coded scopes, making debugging and log analysis easier.

## Features

- **Syntax Highlighting**: Colors timestamps, log levels (TRACE, DEBUG, INFO, WARN, ERROR, FATAL), and messages based on regex patterns.
- **Customizable**: Easily modify the TextMate grammar (`syntaxes/custom-log.tmLanguage.json`) to match your specific log format.
- **Lightweight**: Built with JSON-based TextMate grammars for fast performance, even on large log files.
- **Theme Support**: Leverages VS Code's theme system to style log elements (e.g., errors in red, info in green).
- **Extensible**: Add patterns for IPs, file paths, or custom log structures as needed.

## Installation

1. **Install from VSIX**:
   - Download the `.vsix` file from the Releases section or build it locally (see Development below).
   - In VS Code, go to Extensions (`Ctrl+Shift+X` or `Cmd+Shift+X`), click `...` > Install from VSIX, and select the `.vsix` file.
   - Reload VS Code.
2. **Marketplace** (if published): Search for "Custom Log Highlighter" in the VS Code Extensions Marketplace and click Install.

## Usage

1. Open any `.log` file in VS Code.
2. The extension automatically applies syntax highlighting if the file is recognized as a `Custom Log` language (language mode set to `custom-log` in the bottom-right status bar).
3. If not auto-detected, manually set the language mode:
   - Press `Ctrl+K M` (or `Cmd+K M` on macOS).
   - Select `Custom Log` from the list.

### Example Log Format
The extension highlights logs like this:
```
[2025-09-17 10:00:00] ERROR: Database connection failed
[2025-09-17 10:00:01] INFO: Server started successfully
[2025-09-17 10:00:02] DEBUG: Processing request ID 12345
```
- **Timestamps** (e.g., `[2025-09-17 10:00:00]`) are styled as numeric constants.
- **Log Levels** (e.g., `ERROR`, `INFO`, `DEBUG`) are color-coded (customizable via themes).
- **Messages** (e.g., `Database connection failed`) are treated as strings.

## Configuration

Customize the highlighting by editing `syntaxes/custom-log.tmLanguage.json`. Key sections:
- **Timestamp**: Matches `[YYYY-MM-DD HH:MM:SS]` format. Modify the `match` regex for other formats (e.g., `MM/DD/YYYY`).
- **Log Levels**: Supports `TRACE`, `DEBUG`, `INFO`, `WARN`, `WARNING`, `ERROR`, `FATAL`. Add or remove levels in the `log-level` pattern.
- **Messages**: Captures text after the log level. Adjust the `message` pattern for specific needs.

To debug your grammar:
1. Open a `.log` file.
2. Use the Command Palette (`Ctrl+Shift+P` or `Cmd+Shift+P`) and select **Developer: Inspect Editor Tokens and Scopes**.
3. Click on text to see applied scopes (e.g., `keyword.other.error.custom-log`).

## Development

### Prerequisites
- Node.js (download from [nodejs.org](https://nodejs.org)).
- VS Code.
- `vsce` and `yo` for packaging: `npm install -g vsce yo generator-code`.

### Setup
1. Clone or create the extension:
   ```bash
   mkdir log-highlighter-custom
   cd log-highlighter-custom
   yo code
   ```
   - Select **New Language Support** > **JSON TextMate grammar**.
   - Set:
     - Language ID: `custom-log`
     - Language Name: `Custom Log`
     - File Extensions: `log`
     - Scope Name: `source.custom-log`

2. Install dependencies:
   ```bash
   npm install
   ```

3. Edit `syntaxes/custom-log.tmLanguage.json` to customize patterns (see Usage for examples).

4. Test locally:
   - Press `F5` in VS Code to launch a development instance with the extension loaded.
   - Open a `.log` file to verify highlighting.

5. Package the extension:
   ```bash
   vsce package
   ```
   This creates a `.vsix` file for local installation.

6. Publish (optional):
   - Create a publisher account on the [VS Code Marketplace](https://marketplace.visualstudio.com).
   - Run `vsce publish` to share the extension.

## Contributing

Contributions are welcome! To contribute:
1. Fork the repository (if hosted on GitHub).
2. Create a new branch: `git checkout -b feature/your-feature`.
3. Make changes (e.g., add new patterns to `custom-log.tmLanguage.json`).
4. Test with `npm run test` or `F5`.
5. Submit a pull request.

Report bugs or suggest features via the Issues page.

## License

MIT License. See [LICENSE](LICENSE) for details.

## Resources

- [VS Code Syntax Highlighting Guide](https://code.visualstudio.com/api/language-extensions/syntax-highlight-guide)
- [TextMate Grammar Documentation](https://macromates.com/manual/en/language_grammars)
- [Regex101](https://regex101.com) (use Oniguruma flavor for testing patterns)