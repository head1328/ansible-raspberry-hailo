# Ansible Role: Hailo AI Accelerator

Installs the Hailo AI accelerator driver and runtime for Raspberry Pi AI HAT+ and AI HAT+ 2.

## Supported Hardware

| Device | Variant | TOPS |
|--------|---------|------|
| AI HAT+ (Hailo-8L) | `h8l` | 13 |
| AI HAT+ (Hailo-8) | `h8` | 26 |
| AI HAT+ 2 (Hailo-10H) | `h10` | 40 |

## Requirements

- Raspberry Pi 5
- Debian Trixie (64-bit)
- AI HAT+ or AI HAT+ 2 physically installed

## Installation

```bash
ansible-galaxy role install head1328.hailo
```

## Usage

```yaml
- name: Setup Hailo AI accelerator
  hosts: ai_nodes
  become: true
  roles:
    - role: head1328.hailo
      hailo_variant: h10
```

## Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `hailo_variant` | `h10` | Device variant: `h8l`, `h8`, or `h10` |

## After Installation

The role triggers a reboot when packages are installed. After reboot, verify:

```bash
ls /dev/hailo0
hailortcli fw-control identify
```

## Local Development

Symlink the role into your local Ansible roles path for
development without reinstalling:

```bash
make symlink
```

This creates a symlink at `~/.ansible/roles/head1328.hailo`
pointing to the working directory. Changes are immediately
available to playbooks.

## Testing

Tests require a Raspberry Pi with the Hailo hardware and the Raspberry Pi apt repository configured. The target host is configured via environment variables:

| Variable | Default | Description |
|----------|---------|-------------|
| `MOLECULE_HOST` | (required) | SSH hostname of the test Pi |
| `MOLECULE_USER` | `ansible` | SSH user on the test Pi |

### Test Scenarios

**Full test** (installs packages, verifies installation):

```bash
MOLECULE_HOST=my-pi5 make test
```

**Simulate** (dry-run all variants via `check_mode`, verifies package availability):

```bash
MOLECULE_HOST=my-pi5 make test-simulate
```

**All scenarios**:

```bash
MOLECULE_HOST=my-pi5 make test-all
```

### Other Commands

```bash
MOLECULE_HOST=my-pi5 make converge    # Apply role
MOLECULE_HOST=my-pi5 make verify      # Run verification
make lint                                # Run ansible-lint
```

## License

AGPL-3.0-or-later
