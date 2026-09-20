---
title: 'How to Install Funcionário Infinito'
description: Install, verify, update, and reconfigure Funcionário Infinito in your project
---

Use `npx funcionario-method install` to install Funcionário Infinito in a project, connect it to your
AI coding tool, and update it later.

## When to Use This

- Install Funcionário Infinito in a new or existing project.
- Connect Funcionário Infinito skills to a supported AI coding tool.
- Update an existing Funcionário Infinito installation.
- Add or remove modules, change tools, or reconfigure an installation.

:::note[Prerequisites]

- **Node.js 20.12 or later** is required to run the installer.
- **A supported AI coding tool** is required to use the installed skills. The
  installer can show the current list with `npx funcionario-method install --list-tools`.
- **uv** is required by skills that render or run Python through `uv`, including
  `funcionario-build` and `funcionario-build-auto`. If `uv` is missing, the installer warns
  you but still completes the installation.
- **Git** is required only when you install external modules or custom modules
  from Git.

:::

## Install and verify Funcionário Infinito

### 1. Open the target project

In a terminal, go to the project where you want to install Funcionário Infinito. The installer
uses the current directory unless you choose a different destination.

### 2. Run the installer

```bash
npx funcionario-method install
```

Follow the prompts. The choices can change as modules and tool integrations
change, but the installer guides you through the available modules,
configuration, and supported AI coding tools.

If the installer reports an error or warning, follow the action it gives you.
A missing-`uv` warning does not stop the installation, but skills that require
`uv` will not work until you install it.

### 3. Check the success summary

When the installation finishes, the installer displays **FUNCIONARIO is ready to
use!** and the path where it installed Funcionário Infinito. It also reports any warnings that
still need attention.

### 4. Verify the tool integration

Open your selected AI coding tool from the project directory and invoke the
`funcionario-help` skill. Ask it what to do next. If the tool recognizes and runs the
skill, the integration is ready.

## Update or reconfigure Funcionário Infinito

### 1. Rerun the installer

From the project that contains the `_funcionario` directory, run:

```bash
npx funcionario-method install
```

### 2. Choose the detected path

The installer detects the existing installation and offers the update or
modification paths that apply to it. Choose an update to refresh the existing
setup, or choose modification when you need to change modules, tools, or
configuration. Follow any additional prompts the installer displays. Coming
from an earlier Funcionário Infinito version, the installer also warns about stale `funcionario-*`
entries left in legacy command directories; remove them so your tool does not
show duplicate commands.

### 3. Verify the updated integration

Review the success summary, reopen your AI coding tool if needed, and invoke
`funcionario-help` again.

## Install the prerelease

To install prerelease core and BMM and apply prerelease selection to external
modules chosen in that run, use:

```bash
npx funcionario-method@next install
```

To update a prerelease installation, rerun the same command. Prerelease builds
change more frequently and can include unfinished changes, so use the stable
command for ordinary project work.

## Headless CI installs

For a typical fresh headless install of BMM configured for Claude Code, run:

```bash
npx funcionario-method install --yes --modules bmm --tools claude-code
```

Use `npx funcionario-method install --help` to see the current automation flags and
`npx funcionario-method install --list-tools` to find valid tool IDs. If your
automation uses `@next` or an explicit package version, use that same tag or
version when checking the help and running the installer.

## What You Get

Funcionário Infinito's skills are installed in the skill directories used by each AI tool you
selected. The project's `_funcionario` directory contains shared configuration and
supporting scripts used by those skills. When installation finishes, the
installer reports the configured tools and any warnings that still need
attention.
