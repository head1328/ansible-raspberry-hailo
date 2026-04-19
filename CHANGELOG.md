# Changelog

## 0.2.0

- Add `hailo_source` option to switch between Raspberry Pi
  apt repository (`raspberry`) and Hailo vendor packages
  (`vendor`) from dev-public.hailo.ai
- Add `hailo_vendor_version` and `hailo_vendor_base_url`
  variables for vendor package configuration
- Automatic cleanup of conflicting packages when switching
  between sources (raspberry <-> vendor)
- Fix broken apt state handling during source switches
- Add molecule vendor scenario with idempotence tests
- Add `make symlink` target for local development
- Add local development section to README

## 0.1.0

- Initial release
- Install Hailo driver and runtime via Raspberry Pi apt
  repository
- Support for Hailo-8L, Hailo-8, and Hailo-10H variants
- Molecule test scenarios (default + simulate)
