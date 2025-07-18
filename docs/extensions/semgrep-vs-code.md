---
slug: semgrep-vs-code
title: Visual Studio Code extension
hide_title: true
description: Learn how to install and use Semgrep's extension for Visual Studio Code.
tags:
  - Extensions
---

import IdeLimitations from "/src/components/reference/_ide-limitations.md"
import QuickstartVSCode from "/src/components/procedure/_quickstart-vscode.md"

# Semgrep Visual Studio Code extension

[Semgrep's Visual Studio Code (VS Code) Extension](https://marketplace.visualstudio.com/items?itemName=Semgrep.semgrep) allows you to scan lines when you open and change files in your workspace. It offers:

- Automatic scans whenever you open a file
- Inline results and problem highlighting, as well as quick links to the definitions of the rules underlying the findings
- Autofix, which allows you to apply Semgrep's suggested resolution for the findings

## Prerequisites

- See [Supported Languages](/supported-languages) to verify that the extension supports your project.
- Windows users must use Semgrep VS Code extension v1.6.2 or later.

## Quickstart

<QuickstartVSCode />

## Commands

Run Semgrep extension commands through the [Visual Studio Code Command Palette](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette). You can access the Command Palette using <kbd>Ctrl+⇧Shift+P</kbd> or <kbd>⌘Command+⇧Shift+P</kbd> (macOS). The following list includes all available Semgrep extension commands:

- `Semgrep: Scan all files in a workspace`: Scan all files in the current workspace.
- `Semgrep Search: Clear`: Clear pattern searches from the Primary Side Bar's Semgrep Search view.
- `Semgrep Search: Focus on Search Results View`: Bring the Primary Side Bar's Semgrep Search view into focus
- `Semgrep Restart Language Server`: Restart the language server
- `Semgrep: Scan changed files in a workspace`: Scan files that have been changed since the last commit in your current workspace.
- `Semgrep: Search by pattern`: Search for patterns in code using Semgrep pattern syntax. For more information, see [Pattern syntax](/docs/writing-rules/pattern-syntax) documentation.
- `Semgrep: Show Generic AST`: Show generic AST in a new window
- `Semgrep: Show named Generic AST`: Show named AST in a new window
- `Semgrep: Sign in`: Sign in or log in to the Semgrep AppSec Platform (this command opens a new window in your browser). When you sign in, you can automatically scan with Semgrep [Pro rules](/semgrep-code/pro-rules) and add additional rules to the [Policies](https://semgrep.dev/orgs/-/policies) in Semgrep Code. If you are logged in with the command-line interface using <code>semgrep&nbsp;login</code>, you are also already signed in with the Visual Studio Code Semgrep extension. Alternatively, you can log in through your command-line interface by running `semgrep login`.
- `Semgrep: Sign out`: Log out from Semgrep AppSec Platform. Alternatively, you can sign out through your command-line interface by running `semgrep logout`.
- `Semgrep: Update rules`: For logged-in users. If the rules in the [Policies](https://semgrep.dev/orgs/-/policies) or rules included through the **Semgrep › Scan: Configuration** configuration option have been changed, this command loads the new configuration of your rules for your following scan.

Tip: You can click the Semgrep icon in the Visual Studio Code to access all available commands quickly.

## Additional extension features

Use auto-fix to apply code change suggestions from Semgrep to remediate the security issue.

<video src="https://github.com/returntocorp/semgrep-vscode/assets/626337/3b6a730d-57e9-48a4-8065-9fa52388d77a" controls="controls">
</video>

Add and update new rules to expand Semgrep extension's capabilities.

<video src="https://github.com/returntocorp/semgrep-vscode/assets/626337/fed6b6ec-e0b5-495b-a488-4f3c805dd58b" controls="controls">
</video>

Fine-tune and customize the rules Semgrep uses to improve your scan results:

1. Go to [Semgrep Registry](https://semgrep.dev/explore). Ensure that you are signed in.
2. Explore the Semgrep Registry, select a rule, and then click **Add to Policy**. You can view and manage your rules in [Policies](https://semgrep.dev/orgs/-/policies).
3. Rescan your code. Use <kbd>Ctrl+⇧Shift+P</kbd> or <kbd>⌘Command+⇧Shift+P</kbd> (macOS) to launch the Command Palette, then run `Semgrep: Update rules`.

## Configure the extension

To configure the Semgrep extension, open its **Extension Settings** page:

1. Use <kbd>⇧Shift+Ctrl+X</kbd> or <kbd>⇧Shift+⌘Command+X</kbd> (macOS) to open the **Extensions** view.
2. Select **Semgrep**.
3. Click the **gear** and select **Extension Settings**.

### Configuration options

- **Semgrep › Do Hover**: Enable AST node views when hovering over a finding.
- **Semgrep › Path**: Set the path to the Semgrep executable.
- **Semgrep › Scan: Configuration**: Specify rules or rulesets you want Semgrep to use to scan your code. Each item can be a YAML configuration file, a URL of a configuration file, or a directory of YAML files. Use `auto` to automatically obtain rules tailored to your project. Semgrep uses your project URL to log into the Semgrep Registry. See [Running rules](/docs/running-rules) for more information. Run `Semgrep: Update rules` using the Visual Studio Code Command Palette to update the rules configuration for your following scan whenever you change the rule configuration.
- **Semgrep › Scan: Exclude**: List files and directories that Semgrep should ignore when scanning.
- **Semgrep › Scan: Include**: List files and directories scanned by Semgrep. This option globally overrides the workspace setting. As a result, Semgrep scans all included paths.
- **Semgrep › Scan: Jobs**: Specify how many parallel jobs can run simultaneously. The default number of parallel jobs is one.
- **Semgrep › Scan: Max Memory**: Sets the maximum memory in MB to use.
- **Semgrep › Scan: Max Target Bytes**: Sets the maximum size of the target in bytes to scan.
- **Semgrep › Scan: Only Git Dirty**: Allow Semgrep to scan your code whenever you open a new file and display the findings for lines that have changed since the last commit. On by default.
- **Semgrep › Scan: Pro_intrafile**: Enable intrafile scanning using the Pro Engine.
- **Semgrep › Scan: Timeout**: Set the maximum run time in seconds before Semgrep times out and stops scanning your code. The default value is 30.
- **Semgrep › Scan: Timeout Threshold**: Set the maximum number of rules that can timeout on a file before the file is skipped. If set to 0, there will be no limit. Defaults to 3.
- **Semgrep > Trace: Server**: This option is useful for debugging. The **messages** option displays communication of the Semgrep Visual Studio Code extension with the LSP server. The default option is **verbose**.

### Experimental configuration options

The following experimental features should only be used upon recommendation by Semgrep:

- **Semgrep > Ignore CLI Version**: Ignore the CLI Version and enable all extension features.

## Limitations

<IdeLimitations />

## License

The Semgrep VS Code extension is licensed under the LGPL 2.1 license.
