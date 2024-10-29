# OriginTrail DKG V8 Node Installation Guide
Complete guide for installing OriginTrail DKG V8 node on Ubuntu 24.04 using custom installer

## System Requirements
- 4GB RAM
- 2 CPUs
- 50GB HDD space
- Ubuntu 24.04
- Two wallets (operational and admin) with Base Sepolia ETH

## Pre-Installation Setup

### 1. Update System
```bash
apt update && apt upgrade -y
```

### 2. Configure Firewall
```bash
sudo ufw allow 9999 && sudo ufw allow 8900 && sudo ufw allow 9000 && sudo ufw reload
```

### 3. Install Required Packages
```bash
apt install curl wget git -y
```

## Installation Process

### 1. Download Custom Installer
```bash
wget https://raw.githubusercontent.com/natashyaroo/OriginTrail-DKG-V8-Ubuntu-24.04/main/v8_installer.sh
```

### 2. Make Installer Executable
```bash
chmod +x v8_installer.sh
```

### 3. Run Installer
```bash
./v8_installer.sh
```

## Configuration Details

During installation, you'll need to provide:

1. **Triple Store Selection**
   - Choose Blazegraph (recommended)

2. **Node Configuration**
   ```json
   {
     "network": {
       "hostname": "0.0.0.0",
       "port": 9000,
       "enableRestAPI": true
     },
     "blockchain": {
       "implementations": [
         {
           "network_id": "base-sepolia:11155111",
           "rpc_endpoint_url": "https://base-sepolia-rpc.publicnode.com",
           "hub_contract_address": "0x833F3B6fA34f931c01581FBeE771cd3d40D3c87D"
         }
       ]
     }
   }
   ```

3. **Wallet Details**
   - Operational Wallet private key
   - Admin Wallet address

## Post-Installation

### 1. Check Node Status
```bash
systemctl status otnode
```

### 2. View Logs
```bash
journalctl -u otnode -f
```

### 3. Useful Commands
```bash
# Start node
systemctl start otnode

# Stop node
systemctl stop otnode

# Restart node
systemctl restart otnode
```

## Important Resources

### Network Details
- Network: Base Sepolia Testnet
- RPC Endpoint: https://base-sepolia-rpc.publicnode.com
- Hub Contract: 0x833F3B6fA34f931c01581FBeE771cd3d40D3c87D

### Monitoring
- Testnet Leaderboard: https://dkg-v8-incentivised-testnet.origintrail.io/
- Documentation: https://docs.origintrail.io/dkg-v8-upcoming-version

### Get Test Tokens
1. Join Discord: https://discord.com/invite/QctFuPCMew
2. Request Base Sepolia TRAC tokens from the faucet channel

## Troubleshooting

### Check Ports
```bash
# Verify ports are open
sudo netstat -tulpn | grep -E '8900|9000|9999'

# Check firewall status
sudo ufw status
```

### Common Issues
1. If node fails to start:
   ```bash
   # Check logs for errors
   journalctl -u otnode -n 100
   ```

2. If triple store isn't responding:
   ```bash
   # Restart Blazegraph
   systemctl restart blazegraph
   ```

### Data Directories
- Node configuration: `~/.origintrail_noderc`
- Logs: `/var/log/otnode/`
- Blazegraph data: `/var/lib/blazegraph/`

## Security Recommendations

1. Keep private keys secure and never share them
2. Regularly backup node configuration
3. Monitor system resources
4. Keep Ubuntu system updated
5. Consider setting up monitoring alerts

## Updates

To update the node in the future:
1. Stop the node
   ```bash
   systemctl stop otnode
   ```
2. Run the installer again
3. Start the node
   ```bash
   systemctl start otnode
   ```

## Additional Notes
- Ensure both wallets have sufficient Base Sepolia ETH
- Monitor node performance on the leaderboard
- Join the Discord community for support
- Regularly check for updates and announcements
