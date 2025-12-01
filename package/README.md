# aux4/system-installer-yum

aux4 system installer for yum

This package provides a small aux4 wrapper around the yum package manager so you can manage RHEL/CentOS/Amazon Linux (and other YUM-based) packages via aux4 commands. It exposes install and uninstall actions and maps both the `yum` and `linux` top-level names to the same functionality so it fits naturally into aux4 pkger/system workflows.

Main use cases:
- Quickly install a package from yum inside aux4 workflows and scripts.
- Remove a package using the same simple command path.
- Use as the yum-backed system installer when authoring aux4 packages that list yum as a system installer.

This package is targeted at Linux systems and integrates with the aux4 package manager (it depends on aux4/pkger being available).

## Installation

```bash
aux4 aux4 pkger install aux4/system-installer-yum
```

## Quick Start

Install a package named curl:

```bash
aux4 aux4 pkger system yum install curl
```

This runs yum install -y curl on the host. Run the command as root or prefix with sudo so yum has permission to install packages.

## Install a package

Use this for the common case: installing a single yum package by name.

The command is available at [aux4 aux4 pkger system yum install](./commands/aux4/pkger/system/yum/install).

```bash
aux4 aux4 pkger system yum install <package>
```

Replace <package> with the package name (for example, curl). The command expands to `yum install -y ${package}` and will install the package non-interactively.

## Uninstall a package

Remove a package with the corresponding uninstall action. This maps to `yum remove -y ${package}`.

The command is available at [aux4 aux4 pkger system yum uninstall](./commands/aux4/pkger/system/yum/uninstall).

```bash
aux4 aux4 pkger system yum uninstall <package>
```

Run as root or with sudo so yum can remove packages.

## Using the linux alias

This package exposes the same functionality under the `linux` name (an alias for `yum`) so you can invoke it as:

```bash
aux4 aux4 pkger system linux install curl
```

This is equivalent to `aux4 aux4 pkger system yum install curl` and exists for convenience in workflows that reference "linux" as the system type.

## Examples

### Install curl (minimal)

Install curl non-interactively:

```bash
aux4 aux4 pkger system yum install curl
```

This executes `yum install -y curl`. Use root or sudo to avoid permission errors.

### Remove curl

Uninstall curl:

```bash
aux4 aux4 pkger system yum uninstall curl
```

This executes `yum remove -y curl` and will remove the package non-interactively.

### Use the linux alias

Install wget using the alias:

```bash
aux4 aux4 pkger system linux install wget
```

This is identical to calling the `yum` command and may read more clearly in workflows that use `linux` as the system installer name.

## Requirements

- Platform: linux
- aux4/pkger must be available (this package is intended to be used via aux4's package manager)

## License

This package is licensed under the Apache License 2.0.

See [LICENSE](./license) for details.
