# CCTV Network Security Scanner

A professional-grade Go application for ethical security assessment of CCTV devices on your network.

![Go Version](https://img.shields.io/badge/Go-1.21+-00ADD8?style=flat&logo=go)
![License](https://img.shields.io/badge/license-Educational-blue)
![Status](https://img.shields.io/badge/status-active-success)

## ⚠️ Legal Disclaimer

**IMPORTANT:** This tool is designed for authorized security testing only. Use of this tool on networks you do not own or have explicit written permission to test is **illegal and unethical**. The authors assume no liability for misuse of this software.

## ✨ Features

- 🔍 **Network-wide scanning** - Automatically detect CCTV devices across your network
- 🌐 **Auto-detection** - Smart network interface detection with interactive selection
- 🎯 **Multi-manufacturer support** - Detects Hikvision, Dahua, Axis, Vivotek, Foscam, and more
- 🔐 **Default credential checking** - Tests for common default passwords
- 🛡️ **Vulnerability detection** - Checks for known CVEs and misconfigurations
- 📊 **Comprehensive reporting** - Detailed reports with severity ratings
- 💾 **Export functionality** - Save scan results to timestamped reports
- ⚡ **Concurrent scanning** - Fast multi-threaded network scanning
- 🎨 **Beautiful CLI** - Clean, colorful terminal interface with progress tracking

## 🚀 Quick Start

### Prerequisites

- Go 1.21 or higher
- Network access to devices you want to scan
- Written authorization to scan the target network

### Installation

```bash
# Clone the repository
git clone https://github.com/gatiella/cctv-scanner.git
cd cctv-scanner

# Build the application
go build -o cctv-scanner ./cmd/scanner

# Run the scanner
./cctv-scanner
```

### Installation from Source

```bash
# Install dependencies
go mod download

# Build with optimizations
go build -ldflags="-s -w" -o cctv-scanner ./cmd/scanner
```

## 📖 Usage

### Basic Usage

```bash
./cctv-scanner
```

The scanner will:
1. Display a banner and legal warning
2. Request your authorization confirmation
3. Auto-detect available network interfaces
4. Allow you to select a network or enter manually
5. Scan the selected network range
6. Display comprehensive results
7. Offer to save the report

### Example Session

```
         ╔══════════════════════════════════════════════════════════════╗
         ║                                                              ║
         ║   ██████╗ ██████╗████████╗██╗   ██╗                         ║
         ║  ██╔════╝██╔════╝╚══██╔══╝██║   ██║                         ║
         ║  ██║     ██║        ██║   ██║   ██║                         ║
         ║  ██║     ██║        ██║   ╚██╗ ██╔╝                         ║
         ║  ╚██████╗╚██████╗   ██║    ╚████╔╝                          ║
         ║   ╚═════╝ ╚═════╝   ╚═╝     ╚═══╝                           ║
         ║                                                              ║
         ║           Network Security Scanner v1.0                      ║
         ║           Ethical Security Assessment Tool                   ║
         ║                                                              ║
         ║           ⚡ Developed by: gatiella ⚡                        ║
         ║           🔒 Secure • Fast • Reliable                        ║
         ║                                                              ║
         ╚══════════════════════════════════════════════════════════════╝

⚠️  WARNING: Only use this tool on networks you own or have
   explicit written permission to test.

Do you have authorization to scan this network? (yes/no): yes

🌐 Detected Network Interfaces:
  [1] eth0 - 192.168.1.100 (Network: 192.168.1.0/24)
  [2] wlan0 - 10.0.0.50 (Network: 10.0.0.0/24)
  [M] Enter network range manually

Select an option: 1

✅ Selected network: 192.168.1.0/24
Proceed with this network? (yes/no): yes

🔍 Starting network scan...
This may take a few minutes depending on network size...

📊 Progress: 25.0% (64/256 IPs)
✅ Found device: 192.168.1.45:80
📊 Progress: 50.0% (128/256 IPs)
...
```

## 🏗️ Project Structure

```
cctv-scanner/
├── cmd/
│   └── scanner/
│       └── main.go              # Application entry point
├── internal/
│   ├── scanner/
│   │   └── scanner.go           # Network scanning logic
│   ├── detector/
│   │   └── detector.go          # Device detection
│   ├── checker/
│   │   └── checker.go           # Security checks
│   └── reporter/
│       └── reporter.go          # Report generation
├── pkg/
│   └── models/
│       └── device.go            # Data models
├── configs/
│   └── config.go                # Configuration
├── go.mod                       # Go module definition
├── go.sum                       # Dependency checksums
└── README.md                    # This file
```

## ⚙️ Configuration

Customize the scanner by editing `configs/config.go`:

### Scan Settings
- **Timeout**: Connection timeout (default: 3 seconds)
- **MaxConcurrent**: Maximum concurrent connections (default: 50)
- **CCTVPorts**: Ports to scan (80, 443, 554, 8000, 8080, 8888, 37777, etc.)

### Security Checks
- **CheckDefaultCreds**: Enable/disable default credential testing
- **DefaultCreds**: List of common username/password combinations
- **Manufacturers**: Supported camera manufacturers

### Example Configuration

```go
config := &Config{
    Timeout:           3 * time.Second,
    MaxConcurrent:     50,
    CheckDefaultCreds: true,
    CCTVPorts:         []int{80, 443, 554, 8000, 8080},
}
```

## 🔍 Security Checks

The scanner performs comprehensive security assessments:

### 1. Authentication Issues
- ❌ No authentication required
- 🔑 Default credentials (admin/admin, root/12345, etc.)
- ⚠️ Basic authentication over HTTP
- 🔐 Weak authentication methods

### 2. Encryption Issues
- 🔓 HTTP instead of HTTPS
- 📡 Unencrypted video streams
- 🔒 Missing SSL/TLS certificates
- ⚡ Insecure protocols

### 3. Known Vulnerabilities
- 🐛 CVE-2017-7921 (Hikvision Authentication Bypass)
- 📂 Directory traversal vulnerabilities
- 🔍 Information disclosure
- 🛠️ Configuration file exposure

### 4. Network Exposure
- 🌐 Publicly accessible ports
- 📹 RTSP streams without authentication
- 🔌 UPnP enabled devices
- 🚪 Unnecessary services running

## 📊 Report Output

### Console Output
- Real-time progress tracking
- Device discovery notifications
- Severity-based issue categorization
- Color-coded security ratings
- Actionable remediation steps

### File Output
Automatically timestamped reports:
```
cctv_scan_report_20250110_143022.txt
```

Contains:
- Complete device inventory
- Vulnerability details with severity scores
- Statistics and summaries
- Prioritized recommendations

## 🎯 Supported Devices

### Manufacturers
- Hikvision
- Dahua
- Axis Communications
- Vivotek
- Foscam
- Amcrest
- Lorex
- Swann
- Reolink
- Ubiquiti
- Arlo
- Nest

### Device Types
- IP Cameras
- DVRs (Digital Video Recorders)
- NVRs (Network Video Recorders)
- Video Encoders
- PTZ Cameras

## 🛡️ Ethical Use Guidelines

### ✅ DO:
- Test **only** networks you own
- Obtain **written authorization** before scanning
- Document findings **responsibly**
- Follow **responsible disclosure** practices
- Use results to **improve security**
- Respect **privacy** and **data protection laws**

### ❌ DON'T:
- Scan **unauthorized** networks
- Use findings **maliciously**
- Share vulnerabilities **publicly** without coordination
- **Exploit** vulnerabilities beyond testing scope
- Access or modify **data** without permission
- Violate **local laws** or regulations

## 🔧 Development

### Building from Source

```bash
# Clone repository
git clone https://github.com/gatiella/cctv-scanner.git
cd cctv-scanner

# Install dependencies
go mod download

# Run tests (when available)
go test ./...

# Build
go build -o cctv-scanner ./cmd/scanner
```

### Cross-Platform Builds

```bash
# Linux
GOOS=linux GOARCH=amd64 go build -o cctv-scanner-linux ./cmd/scanner

# Windows
GOOS=windows GOARCH=amd64 go build -o cctv-scanner.exe ./cmd/scanner

# macOS
GOOS=darwin GOARCH=amd64 go build -o cctv-scanner-mac ./cmd/scanner
```

### Code Formatting

```bash
# Format all code
go fmt ./...

# Run linter
go vet ./...
```

## 🤝 Contributing

Contributions are welcome! Please ensure all additions maintain ethical use standards.

### How to Contribute

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Guidelines
- Maintain code quality and formatting
- Add tests for new features
- Update documentation
- Follow ethical hacking principles
- Respect the project's security focus

## 📝 License

This tool is provided for **educational and authorized security testing purposes only**. 

By using this software, you agree to:
- Use it only on networks you own or have explicit permission to test
- Comply with all applicable laws and regulations
- Not use it for malicious purposes
- Accept full responsibility for your actions

## 🐛 Troubleshooting

### Common Issues

**Issue**: Permission denied when running scanner
```bash
chmod +x cctv-scanner
```

**Issue**: No devices found
- Verify network range is correct
- Check firewall settings
- Ensure devices are powered on
- Verify network connectivity

**Issue**: Slow scanning
- Reduce MaxConcurrent in config
- Increase Timeout value
- Check network bandwidth

## 📞 Support

For issues, questions, or feature requests:
- 🐛 [Open an Issue](https://github.com/gatiella/cctv-scanner/issues)
- 💬 [Discussions](https://github.com/gatiella/cctv-scanner/discussions)
- 📧 Contact: [Your Email]

## 🙏 Acknowledgments

- Thanks to the Go community
- Inspired by various network security tools
- Built with ethical hacking principles in mind

## ⚖️ Responsible Disclosure

If you discover a security vulnerability in this tool, please report it responsibly:
1. **Do not** publish the vulnerability publicly
2. Contact the maintainers privately
3. Allow time for a fix to be developed
4. Coordinate public disclosure

---

**Remember**: With great power comes great responsibility. Use this tool ethically and legally.

(https://github.com/EnUs13}