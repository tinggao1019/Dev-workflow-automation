# Dev-workflow-automation
Automation toolkit with AI-powered git analysis, auto-formatting (C/C++/JSON), batch file modification, and custom tool execution through Copilot Chat integration

# Common Tools Chat Extension

A VS Code extension that provides a Chat Participant for GitHub Copilot, allowing you to interact with common tools and perform AI-powered file analysis with git history insights.

## Features

- **Chat Participant**: Interact with `@commonTools` in GitHub Copilot Chat
- **Tool Discovery**: Use `/listTools` to see all available tools
- **Tool Execution**: Use `/runTool` to execute specific tools with parameters
- **AI File Analysis**: Analyze current file's git history and related files with AI insights
- **Git Integration**: Access repository information and file change history
- **Natural Language**: Ask questions about tools in plain English

## Usage

### Chat Interface
1. Open GitHub Copilot Chat
2. Type `@commonTools` to start interacting with the Common Tools agent
3. Use commands:
   - `/listTools` - Show all available tools
   - `/runTool tool: ToolName, params: {param: value}` - Run a specific tool
   - `/gitInfo` - Show Git repository information
   - `/analyzeFile` - Analyze current file's git history and find related files
   - `/analyzeCommits <sha1> <sha2>...` - Analyze specific commits and answer questions
   - Or just ask naturally: "Show me available tools" or "Analyze this file"

### File Analysis with AI

The `/analyzeFile` command provides comprehensive analysis of your current file:

**What it does:**
```
@commonTools /analyzeFile
```

**Provides:**
- 📜 Recent git commit history (last 10 commits)
- 🔗 Related files (files changed together with this file)
- 🤖 AI-powered analysis including:
  - File purpose and functionality
  - Change patterns and trends
  - Important related files and dependencies
  - Potential concerns and recommendations

### Analyze Specific Commits

The `/analyzeCommits` command analyzes specific commits and answers your questions:

**What it does:**
```
@commonTools /analyzeCommits abc1234 def5678 What changed in these commits?
@commonTools /analyzeCommits 9a8b7c6 Why was this function modified?
```

**Provides:**
- 📋 Detailed information for each commit (author, date, message)
- 📝 Actual code changes/diffs for the current file
- 🤖 AI-powered analysis that:
  - Explains what changed in the specified commits
  - Compares changes with current file state
  - Answers your specific question about the commits
  - Identifies patterns and potential issues

**Example Output:**
```
## 🔍 Analyzing Commits for: `myfile.cpp`

Found 2 commit hash(es): `abc1234`, `def5678`

### 📋 Commit Details
1. **Fix memory leak in buffer allocation**
   - Hash: `abc1234`
   - Author: John Doe
   - Date: 2025-11-23

2. **Refactor initialization logic**
   - Hash: `def5678`
   - Author: Jane Smith
   - Date: 2025-11-22

### 🤖 AI Analysis
The commits show a progression from fixing a memory leak...
```

**Example Output:**
```
## 📄 Analyzing: `myfile.cpp`

### 📜 Recent Git History (5 commits)
1. **Fix memory leak in buffer allocation**
   - Author: John Doe
   - Date: 2025-11-23
   - Hash: `abc12345`

### 🔗 Related Files (12 files)
- `include/buffer.h`
- `src/memory_manager.cpp`
- `tests/buffer_test.cpp`

### 🤖 AI Analysis
Based on the git history and related files, this appears to be...
```

### Git Repository Information
```
@commonTools /gitInfo
```
Shows:
- Repository path
- Current branch
- Latest commit
- Upstream branch
- Remote repositories

### Traditional Commands
1. Press `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (macOS)
2. Type **"Run Common Tool"**
3. Pick a tool from the menu
4. Output appears in notifications

## Commands Available

The extension provides these VS Code commands:
- `Run Common Tool (interactive)` - Interactive tool selection
- `Run Common Tool (direct)` - Direct tool execution with parameters  
- `List Common Tools` - Show all available tools
- `Modify Files` - Batch modify files based on configuration

## Configuration

### Tool Configuration
Tools are defined in `commands.json` in the extension directory. Each tool can have:
- `title`: Display name
- `shell`: Command to execute
- `params`: Optional parameters with prompts

### Workspace Settings
Configure in `.vscode/settings.json`:
```json
{
  "commonTools.filesToModify": ["file1.h", "file2.cpp"],
  "commonTools.searchFolder": "src/include",
  "commonTools.insertContent": "#define CqiData_orig"
}
```

## Dependencies

### Required
- **vscode.git**: Built-in Git extension (included with VS Code)
- **git**: Git must be installed and available in your PATH

### Optional
- None - all features work with built-in VS Code functionality

## Example

```
User: @commonTools show me all tools
Agent: Here are all available common tools:
1. Format Changed C/C++ Files
2. Build sct case (Parameters: param)
3. Run single UT (Parameters: param)

User: @commonTools analyze this file
Agent: 📄 Analyzing: `extension.js`

### 📜 Recent Git History (3 commits)
1. **Add file analysis feature**
   - Author: tinggao1019
   - Date: 2025-11-24
   
### 🔗 Related Files (8 files)
- `package.json`
- `README.md`
- `commands.json`

### 🤖 AI Analysis
This file serves as the main extension entry point...
The recent changes show a pattern of adding new features...

User: @commonTools /analyzeCommits abc1234 def5678 What was the purpose of these changes?
Agent: 🔍 Analyzing Commits for: `extension.js`

### 📋 Commit Details
1. **Add commit analysis feature**
2. **Fix error handling**

### 🤖 AI Analysis
These commits introduced a new feature for analyzing specific commits.
The first commit (abc1234) added the core functionality...
The second commit (def5678) improved error handling...
```

## Adding Commands

1. Edit `commands.json`
2. Reload the VS Code window

## Packaging

```bash
npm install
npx vsce package
```

## Files

- `extension.js` - Main extension code with ChatParticipant and git analysis
- `commands.json` - Tool definitions
- `package.json` - Extension manifest
- `LICENSE` - MIT License

