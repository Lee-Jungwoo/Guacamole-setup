# Guacamole VNC Setup Script

This script automatically sets up and deploys a complete remote desktop environment using Apache Guacamole, TigerVNC Server, and XFCE desktop environment on Ubuntu.

## What This Script Does

This comprehensive setup script performs the following operations:

### Core Services Installation & Configuration
- **Apache Guacamole**: Installs and configures Guacamole server (1.5.5) for web-based remote desktop access
- **TigerVNC Server**: Sets up VNC server for remote desktop connections
- **XFCE Desktop Environment**: Installs lightweight desktop environment optimized for remote access
- **Nginx Web Server**: Configures reverse proxy to serve Guacamole web client with SSL support
- **MariaDB Database**: Sets up database backend for Guacamole user management and connection storage

### Security & SSL Configuration
- **SSL/TLS Encryption**: Automatically configures HTTPS using Let's Encrypt certificates via Certbot
- **Firewall Configuration**: Opens necessary ports (80, 443) for web access
- **Database Security**: Secures MariaDB installation with default security settings

### Development Environment
- **Visual Studio Code**: Installs VS Code with desktop shortcut
- **Firefox Browser**: Installs Firefox browser with desktop shortcut and snap workarounds
- **Korean Language Support**: Installs Korean fonts (Nanum, D2Coding) and input method (ibus-hangul)

### User Experience Enhancements
- **Desktop Shortcuts**: Creates desktop shortcuts for Firefox and VS Code
- **Auto-startup Scripts**: Configures automatic execution of maintenance tasks on login
- **VNC Session Optimization**: Sets up proper X11 forwarding and session management

## Requirements

- **Operating System**: Ubuntu 22.04 LTS (fresh installation)
- **System Access**: Root/sudo privileges required
- **Network**: Internet connection for package downloads and certificate generation
- **Domain/Hostname**: Valid domain name or hostname for SSL certificate generation
- **Email Address**: Valid email address for Let's Encrypt certificate registration

## How to Use This Script

### Installation Steps
1. **Download the script**:
   ```bash
   wget -L https://raw.github.com/lee-jungwoo/Guacamole-setup/main/init.sh
   # or clone the repository
   git clone https://github.com/Lee-Jungwoo/Guacamole-setup.git
   cd Guacamole-setup
   ```

2. **Make the script executable**:
   ```bash
   (sudo) chmod +x init_native.sh
   ```

3. **Run the installation script**:
   ```bash
   ./init.sh
   ```

4. **Enter your hostname and valid email**
   - Requesting SSL certificate with certbot requires hostname and email.

5. **During Installation:**
   - The script will automatically handle most user prompts
   - Some installations may require brief user interaction, depending on the environment
   - MySQL root password is set to `1234`
   - VNC password is set to `123456`
   

### Post-Installation Access

#### Web Access (Recommended)
- **URL**: `https://[your-domain]/guacamole` (or `http://[your-domain]/guacamole` which redirects to HTTPS)
- **Default Credentials**:
  - Username: `guacadmin`
  - Password: `guacadmin` (change this to your own right after first login)

## Default Configuration

### MariaDB Database Settings
- **Database Name**: `guac_db`
- **Database User**: `guac_user`
- **Database Password**: `1234`
- **MySQL Root Password**: `1234`

### VNC Configuration
- **Display**: `:1` (port 5901)
- **Password**: `123456`
- **Desktop Environment**: XFCE4

### Network Configuration
- **HTTP Port**: 80 (redirects to HTTPS)
- **HTTPS Port**: 443
- **Guacamole server**: 8080 (internal)
- **VNC Port**: 5901 (localhost only)

## Troubleshooting

### Common Issues
1. **Certificate Generation Fails**: Ensure your domain points to the server's IP address
2. **VNC Connection Issues**: Check if VNC server is running with `vncserver --list`
3. **Web Interface Not Loading**: Verify nginx and tomcat9 services are running<br>
`sudo systemctl status nginx tomcat9 mysql guacd`<br>
stop and restart them if they are halt.<br>
`sudo systemctl stop nginx tomcat9 guacd mysql` <br>
`sudo systemctl stop nginx tomcat9 guacd mysql`

4. **Database Connection Errors**: Check MariaDB service status and credentials

### Service Management
```bash
# Check service status
sudo systemctl status nginx guacd tomcat9 mysql

# Restart services
sudo systemctl restart nginx guacd tomcat9 mysql

# Check VNC server
tigervncserver -list
```

### Log Files
- **Nginx**: `/var/log/nginx/`
- **Tomcat**: `/var/log/tomcat9/`
- **Guacamole**: `/var/log/tomcat9/catalina.out`
- **MySQL**: `/var/log/mysql/`

## Security Notes

⚠️ **Important Security Considerations**:
- Change default passwords immediately after installation
- The script removes the password for the `ubuntu` user account
- Default database passwords are weak and should be changed if needed
- Consider implementing additional firewall rules for production use
- SSL certificates are automatically renewed by certbot

## Support

For issues or questions:
- Check the troubleshooting section above
- Review log files for error messages
- Ensure all requirements are met
- Verify network connectivity and DNS resolution

---

**Note**: This script is designed for development and testing environments. For production deployments, review and modify security settings, passwords, and configurations according to your organization's security policies.

**Disclaimer**: The author of this script assumes no responsibility for any legal or technical issues arising from its use.
