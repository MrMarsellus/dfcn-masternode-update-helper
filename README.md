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
- Safety-first stop logic: ensures daemon and systemd service are fully stopped (including hard kill if needed) before installing new binaries.  
- Post-start health checks: verifies service state, RPC availability and basic masternode status after restart, and reports if warnings were detected.  

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
- A systemd service for the daemon (default: `defcond.service`).  
  The script will stop and disable this service before updating and enable and start it again afterwards.

## Exit status and result messages

At the end of a run the script prints a short summary:

- `Script run completed successfully. Update completed successfully.`  
  The update or rollback was installed and post-start health checks did not report any issues.

- `Script run completed with warnings. Update was installed, but post-start checks reported warnings.`  
  Binaries were installed and the service was restarted, but RPC or masternode status did not look fully healthy yet. You should inspect the node and logs.

If a critical step fails (for example safe stop cannot be confirmed, installation fails, or the service cannot be started), the script aborts with a non-zero exit code and points you to the logfile.

## Notes

The script is interactive and will guide you through update, rollback, or backup cleanup from its menu. It also performs checks before and after the binary installation to help confirm that the masternode is running again.

After restart the script runs lightweight RPC health checks (`getbestblockhash`, `getblockcount`, `getnetworkinfo`, `mnsync`, `masternode status`). These checks do not modify any state; they only help you confirm that the node came back in a healthy condition.
