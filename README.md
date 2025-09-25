# Remote Access Workflow

This repository provides GitHub Actions workflows that enable remote access to both Windows and Linux GitHub-hosted runners using Tailscale for secure networking.

## Features

- **Cross-platform support**: Works on both Windows and Linux
- **Secure networking**: Uses Tailscale for secure remote connections
- **Multiple access methods**:
  - Windows: RDP (Remote Desktop Protocol)
  - Linux: SSH + VNC (with XFCE4 desktop environment)
- **Flexible deployment**: Choose to run on Windows only, Linux only, or both

## Prerequisites

1. **Tailscale Account**: You need a Tailscale account and auth key
2. **GitHub Secrets**: Add your Tailscale auth key as a secret named `TAILSCALE_AUTH_KEY`

## Usage

1. Go to the "Actions" tab in your GitHub repository
2. Select the "Remote Access" workflow
3. Click "Run workflow"
4. Choose your operating system:
   - `windows`: Run only on Windows runners
   - `linux`: Run only on Linux runners  
   - `both`: Run on both Windows and Linux runners (default)

## Access Methods

### Windows (RDP)
- **Protocol**: Remote Desktop Protocol (RDP)
- **Port**: 3389
- **Client**: Any RDP client (Windows Remote Desktop, Microsoft Remote Desktop, etc.)
- **Connection**: Use the Tailscale IP provided in the workflow output
- **Credentials**: Username and password will be displayed in the workflow logs

### Linux (SSH + VNC)
- **SSH Access**:
  - **Port**: 22
  - **Command**: `ssh remoteuser@<tailscale-ip>`
  - **Password**: Displayed in workflow logs
- **VNC Access**:
  - **Port**: 5901
  - **Server**: `<tailscale-ip>:5901`
  - **Client**: Any VNC client (RealVNC, TightVNC, etc.)
  - **Password**: Displayed in workflow logs
  - **Desktop**: XFCE4 desktop environment

## Security Features

- Passwords are randomly generated for each session
- Tailscale provides encrypted mesh networking
- Runners are isolated and temporary
- Connections are only accessible through your Tailscale network

## Workflow Timeout

The workflow runs for up to 6 hours (3600 minutes) or until manually cancelled. To stop the workflow, go to the Actions tab and cancel the running workflow.

## Troubleshooting

- Ensure your `TAILSCALE_AUTH_KEY` secret is properly configured
- Check workflow logs for connection details and any error messages
- Verify your Tailscale network allows the runner to connect
- For VNC issues, ensure your VNC client supports the connection format `ip:5901`