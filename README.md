# DeFCoN Masternode Binary Updater

Interactive Bash helper script for updating DeFCoN masternode binaries on a VPS. It is intended for already installed DeFCoN masternodes and supports binary updates, rollback, backup cleanup, logfile output, dry-run testing, and automatic rollback if the updated daemon fails to start.

## Features

- Binary update. 
- Binary rollback. 
- Backup cleanup. 
- Automatic backup of the current binaries before installing an update. 
- Logfile output for every run. 
- Dry-run mode for safe testing without destructive changes. 
- Automatic rollback if the updated daemon fails to start. 
- Auto-rollback can be disabled with `--no-auto-rollback`. 

## Download and run

```bash
cd /root && curl -fsSLo defcon-binary-updater.sh https://raw.githubusercontent.com/MrMarsellus/dfcn-masternode-update-helper/main/defcon-binary-updater && chmod +x defcon-binary-updater.sh && sudo ./defcon-binary-updater.sh
```

## Dry-run

Recommended before first live use. Dry-run is useful because it shows the planned actions without making destructive changes. 

```bash
cd /root && curl -fsSLo defcon-binary-updater.sh https://raw.githubusercontent.com/MrMarsellus/dfcn-masternode-update-helper/main/defcon-binary-updater && chmod +x defcon-binary-updater.sh && sudo ./defcon-binary-updater.sh --dry-run
```

## Disable auto-rollback

Automatic rollback is enabled by default. If you do not want the script to restore the previous binaries automatically after a failed start, use: 

```bash
cd /root && curl -fsSLo defcon-binary-updater.sh https://raw.githubusercontent.com/MrMarsellus/dfcn-masternode-update-helper/main/defcon-binary-updater && chmod +x defcon-binary-updater.sh && sudo ./defcon-binary-updater.sh --no-auto-rollback
```

## Raw URL

```text
https://raw.githubusercontent.com/MrMarsellus/dfcn-masternode-update-helper/main/defcon-binary-updater
```

## Requirements

- Linux VPS. 
- Existing DeFCoN masternode installation.
- Root access.

## Notes

The script is interactive and will guide you through update, rollback, or backup cleanup from its menu. It also performs checks before and after the binary installation to help confirm that the masternode is running again.
