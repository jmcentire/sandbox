# Sandbox CLI Tool

The **sandbox** script creates an isolated chroot based environment with optional network access.  It copies a minimal set of binaries and configuration files so you can experiment without affecting the host system.

## Features

- Chroot based sandbox with optional network isolation
- Mount a host directory inside the sandbox at `/mnt`
- Automatically install Python packages from a configuration file
- Copies git configuration and SSH keys so tools like `git` work inside the sandbox
- Configurable via an INI style configuration file

## Installation

Clone this repository and make the `sandbox` script executable:

```bash
chmod +x sandbox
```

## Requirements

- Linux is fully supported. macOS can run the script with limited features
  because `chroot` and namespace tools are restricted.
- Binaries are located using the `which` command rather than assuming fixed
  paths.

## Usage

```bash
./sandbox [OPTIONS]
```

Options:

- `--config FILE` – Path to a configuration file. If omitted, defaults are used.
- `--mnt DIRECTORY` – Host directory to mount at `/mnt` inside the sandbox.
- `--create-sample-config` – Write an example configuration file `sb.conf.example` and exit.

## Configuration File

The configuration uses INI sections.  See `sb.conf.example` for a complete example.  Relevant sections include:

- `[network]` – Control allowed ports and IP ranges.
- `[packages]` – Python packages to install on startup.
- `[applications]` – Additional system applications to copy into the sandbox.
- `[ssh]` – Comma separated list of SSH key file names to copy into the sandbox.  When omitted, all keys found in `~/.ssh` or the mounted directory are copied.
- `[environment]` – Extra environment variables.
- `[profile]` – Custom shell commands to run when the sandbox starts.

## License

This project is licensed under the MIT License.  See [LICENSE](LICENSE) for details.
