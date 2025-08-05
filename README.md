# WASFixer - Windows Audio Services Fixer

A lightweight, professional Windows service that actively prevents the Windows Audio service from being stopped or disabled. Built with native WinAPI for maximum efficiency and minimal resource usage.

## 🎯 Purpose

WASFixer solves the common problem where the Windows Audio service (`Audiosrv`) gets stopped randomly or accidentally by other applications, causing audio to stop working. The service continuously monitors the audio service and immediately restarts it if it detects any stop attempts.

## ⚠️ Disclaimer

**Windows Only**: This software is designed specifically for Windows operating systems (10/11) and will not work on macOS, Linux, or other operating systems. The service uses Windows-specific APIs and registry functions that are not available on other platforms.

**Administrator Rights Required**: The service requires Administrator privileges to function properly, as it needs to control Windows system services.

## 📦 Installation

### **Automatic Installation**
1. Download and run `WASFixerSetup.exe`
2. Follow the installation wizard
3. Service starts automatically after installation

## 🗑️ **Uninstallation**
### **Automatic Uninstallion:**
1. Navigate to: `C:\Program Files\Windows Audio Services Fixer\`
2. Run `unins000.exe` (or similar uninstaller executable)
3. Follow the uninstallation wizard

### **Manual Cleanup (if needed):**
1. Stop the `WASFixer.exe` process in Task Manager
2. Delete the installation folder: `C:\Program Files\Windows Audio Services Fixer\`
3. Delete the log folder: `C:\ProgramData\AudioFix\`

## 🚀 Usage

### **Running the Service**
It runs automatically

### **Force Starting the Service (manually, if needed)** 
1. Open Command Prompt as Administrator
2. Navigate to the installation directory:
   ```batch
   cd "C:\Program Files\Windows Audio Services Fixer"
   ```
   or wherever you downloaded to
3. Type:
   ```batch
   WASFixer.exe
   ```
4. Hit Enter to start the service

## ✨ Features

### **Minimal Resource Usage**
- **Memory**: Less than 5MB RAM when idling
- **CPU**: Less than 0.1% CPU usage
- **Disk**: Lightweight 19KB executable
- **Background**: Runs silently without console window
  
### **Active Prevention**
- **Real-time monitoring**: Checks audio service status every second
- **Preventive action**: Detects stop attempts and immediately counteracts them
- **State tracking**: Distinguishes between "stopping" and "stopped" states
- **Immediate response**: Restarts service within 1 second of detection

### **Professional Logging**
- **UTF-16 encoded logs**: Proper Unicode support
- **Automatic rotation**: 10KB log size limit with backup
- **Structured logging**: Timestamped entries with detailed status
- **Error tracking**: Comprehensive error logging with Windows error codes

### **Enterprise Features**
- **Static linking**: No DLL dependencies
- **Administrator privileges**: Proper service control access
- **Professional installer**: Inno Setup with multi-language support
- **Auto-start**: Registry integration for automatic startup

## 🛠️ Technical Details

### **Architecture**
- **Language**: C with native WinAPI calls
- **Compilation**: GCC with size optimization (`-Os`)
- **Linking**: Static linking for portability
- **Subsystem**: Windows GUI (no console window)

### **Key Components**
- **Service Control Manager**: Direct WinAPI access for service operations
- **File I/O**: Native Windows file operations for logging
- **Process Management**: Low priority background operation
- **Error Handling**: Comprehensive error checking and recovery

### **Monitoring Logic**
1. **Every second**: Check if `Audiosrv` is running
2. **If stopping detected**: Immediately attempt to restart
3. **If already stopped**: Log as critical and restart
4. **State tracking**: Monitor transitions for detailed logging

## 📊 Performance Metrics

### **Resource Usage**
- **Memory**: ~5MB RAM (idle)
- **CPU**: <0.1% (normal operation)
- **Disk I/O**: Minimal (log rotation only)
- **Network**: None

### **Response Times**
- **Detection**: <1 second
- **Restart**: <2 seconds
- **Logging**: Immediate with file flush

## 📝 Logging

### **Log Location**
```
C:\ProgramData\WASFixer\WASFixer.log
```

### **Log Format**
```
[2024-01-15 14:30:25] Service started
[2024-01-15 14:30:26] Service is running normally
[2024-01-15 14:35:12] WARNING: Service is being stopped! Attempting to prevent shutdown
[2024-01-15 14:35:13] Service started successfully
```

### **Log Rotation**
- **Max size**: 10KB
- **Backup**: `WASFixer.log.bak`
- **Encoding**: UTF-16 LE with BOM
- **Flushing**: Immediate disk writes

### **Verification**
1. Check Task Manager for `WASFixer.exe` process
2. Monitor log file for activity
3. Test by attempting to stop Windows Audio service

## 🔍 Troubleshooting

### **Common Issues**

**Service won't start:**
- Ensure running as Administrator
- Check Windows Event Log for errors
- Verify `Audiosrv` service exists

**Log file not created:**
- Check `C:\ProgramData\WASFixer\` permissions
- Ensure Administrator privileges
- Verify disk space

**Audio still stops:**
- Check log file for error messages
- Verify service is actually running
- Test with manual service stop

### **Debug Information**
- **Log file**: `C:\ProgramData\AudioFix\audioFix.log`
- **Process**: Check Task Manager for `WASFixer.exe`
- **Registry**: `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`

## 🛡️ Security

### **Permissions Required**
- **Administrator**: For service control operations
- **File system**: Write access to `C:\ProgramData\`
- **Registry**: Read/write access for startup integration

### **Safety Features**
- **Read-only service queries**: No modification of other services
- **Minimal privileges**: Only what's necessary for audio service control
- **Error handling**: Graceful degradation on permission issues


## 📄 License

This project is developed by Tanmay Malik. The service is designed for personal and enterprise use to maintain Windows audio functionality.

## 🤝 Contributing

The project is focused on reliability and minimal resource usage. Any improvements should maintain these core principles:
- Minimal memory footprint
- Low CPU usage
- Robust error handling
- Professional logging

---

**Version**: 1.0  
**Author**: Tanmay Malik  
**Platform**: Windows 10/11 (x64)  
**License**: Personal/Enterprise Use 
