# OriginTrail Node Installation Guide for Ubuntu 24.04

This repository contains an installation script for setting up an OriginTrail node on Ubuntu 24.04 LTS. This is an updated version that extends support from previous Ubuntu 20.04/22.04 versions to include Ubuntu 24.04.

## Prerequisites

- A clean Ubuntu 24.04 LTS installation
- Root access or sudo privileges
- Minimum system requirements:
  - 4 CPU cores
  - 8GB RAM
  - 100GB SSD storage
- Required ports:
  - 8900 (OriginTrail API)
  - 9000 (P2P node communication)
  - 9999 (Blazegraph)

## Initial Server Setup

### Firewall Configuration

Configure the necessary ports using UFW (Uncomplicated Firewall):

```bash
sudo ufw allow 9999 && sudo ufw allow 8900 && sudo ufw allow 9000 && sudo ufw reload
```

## Features

- Automated installation of all required dependencies
- Support for both Blazegraph and Fuseki triple stores
- MySQL/MariaDB database setup
- Configurable node settings
- Base Sepolia (Testnet) blockchain integration
- Systemd service configuration
- Convenient command aliases

## Quick Installation

1. Download the installation script:
```bash
wget -q https://raw.githubusercontent.com/[your-repo]/install-ubuntu-24.04.sh
```

2. Make it executable:
```bash
chmod +x install-ubuntu-24.04.sh
```

3. Run the script:
```bash
sudo ./install-ubuntu-24.04.sh
```

## Installation Options

During installation, you'll be prompted to choose:

1. Triple Store Database:
   - Blazegraph (Default)
   - Fuseki
   
2. SQL Database:
   - MySQL (Default)
   - MariaDB

3. Node Configuration:
   - Operator fee (0-100%)
   - Operational wallet details
   - Management wallet address
   - Profile shares token details
   - RPC endpoint configuration

### RPC Configuration

The default RPC endpoint for Base Sepolia testnet:
```
https://base-sepolia-rpc.publicnode.com
```

## Command Aliases

After installation, the following aliases are available:
- `otnode-restart` - Restart the node service
- `otnode-stop` - Stop the node service
- `otnode-start` - Start the node service
- `otnode-logs` - View node logs
- `otnode-config` - Edit node configuration

To start using the aliases, run:
```bash
source ~/.bashrc
```

## Service Management

The installation creates a systemd service for managing the node. You can manage it using:
```bash
systemctl start otnode
systemctl stop otnode
systemctl restart otnode
systemctl status otnode
```

## Configuration

The main configuration file is located at:
```
~/ot-node/.origintrail_noderc
```

## Logging

To view the node logs:
```bash
journalctl -u otnode --output cat -f
```

## Monitoring and Resources

### Testnet Leaderboard
Monitor your node's performance on the incentivized testnet:
```
https://dkg-v8-incentivised-testnet.origintrail.io/
```

### Documentation
Comprehensive documentation for DKG v8:
```
https://docs.origintrail.io/dkg-v8-upcoming-version
```

## Important Notes

1. The installer is specifically designed for Ubuntu 24.04 LTS and won't work on other versions
2. Backup any existing configuration before running the installer if you're upgrading
3. Make sure to properly secure your server and keep your private keys safe
4. The node is configured for Base Sepolia (Testnet) by default
5. Ensure all required ports (8900, 9000, 9999) are properly configured in your firewall

## Troubleshooting

If you encounter any issues:

1. Check the logs using `otnode-logs`
2. Ensure all services are running:
   ```bash
   systemctl status otnode
   systemctl status blazegraph # or fuseki
   systemctl status mysql # or mariadb
   ```
3. Verify your configuration in `.origintrail_noderc`
4. Check firewall status and port accessibility:
   ```bash
   sudo ufw status
   sudo netstat -tulpn | grep -E '8900|9000|9999'
   ```

## Updates

To update your node in the future:

1. Stop the node service:
   ```bash
   otnode-stop
   ```
2. Run the installer again
3. Choose whether to keep or overwrite existing configurations

## Support

For additional help and support:
- Visit the official documentation: https://docs.origintrail.io
- Join the OriginTrail Discord community
- Check the GitHub repository issues section
- Refer to DKG v8 documentation: https://docs.origintrail.io/dkg-v8-upcoming-version

## License

This installation script is released under the [Apache 2.0 License](LICENSE).
