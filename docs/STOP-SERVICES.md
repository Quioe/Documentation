# quieo Service Management - Stop Scripts

This document describes the various scripts available to stop quieo services and processes across different platforms.

## 📋 Available Stop Scripts

### 1. **Recommended Scripts**

| Script | Platform | Features | Best For |
|--------|----------|----------|----------|
| `stop.py` | Cross-platform | Advanced process detection, graceful shutdown | Production use |
| `stop.sh` | Linux/macOS | Comprehensive service stopping | Unix systems |
| `stop.bat` | Windows | Full Windows support | Windows systems |

### 2. **Emergency Scripts**

| Script | Platform | Features | Best For |
|--------|----------|----------|----------|
| `emergency-stop.sh` | Linux/macOS | Force-kill all processes immediately | Critical situations |
| `emergency-stop.bat` | Windows | Force-kill all processes immediately | Critical situations |

## 🚀 Quick Usage

### Normal Shutdown (Recommended)
```bash
# Cross-platform (Python)
python3 stop.py

# Linux/macOS
./stop.sh

# Windows
stop.bat
```

### Emergency Shutdown
```bash
# Linux/macOS
./emergency-stop.sh

# Windows
emergency-stop.bat
```

## 📖 Detailed Usage

### Python Stop Script (`stop.py`)

The most advanced and recommended stopping script with cross-platform support.

**Basic Usage:**
```bash
python3 stop.py                    # Stop all services
python3 stop.py --docker-only      # Stop only Docker services
python3 stop.py --list             # List quieo processes
python3 stop.py --force            # Force-kill processes
python3 stop.py --help             # Show help
```

**Features:**
- ✅ Cross-platform compatibility (Windows, Linux, macOS)
- ✅ Advanced process detection using `psutil`
- ✅ Graceful shutdown with fallback to force-kill
- ✅ Comprehensive service identification
- ✅ Real-time status reporting
- ✅ Safe temporary file cleanup

### Shell Stop Script (`stop.sh`)

Comprehensive bash script for Unix systems.

**Usage:**
```bash
./stop.sh                          # Stop all services
./stop.sh --docker-only            # Stop only Docker services  
./stop.sh --force                  # Force-kill all processes
./stop.sh --help                   # Show help
```

**Features:**
- ✅ Colored terminal output
- ✅ Step-by-step process reporting
- ✅ Docker container cleanup
- ✅ Graceful and force termination options
- ✅ Process verification

### Batch Stop Script (`stop.bat`)

Windows-specific batch script.

**Usage:**
```cmd
stop.bat                           # Stop all services (interactive)
```

**Features:**
- ✅ Windows process management
- ✅ Docker container cleanup  
- ✅ Interactive status display
- ✅ Option to show remaining processes
- ✅ Comprehensive service termination

## 🔍 What Gets Stopped

All stop scripts terminate the following services:

### Docker Services
- All Docker Compose services defined in `docker-compose.yml`
- quieo-related containers (`quieo*`, `quantum*`, `mailhog`)
- Orphaned containers

### Desktop Applications
- **Nextron Desktop UI** (Electron processes)
- **UI development server** (`npm run dev` in `ui-app/`)

### Node.js Services
- **Sender service** (`sender/sender.js`)
- **Receiver service** (`receiver/receiver.js`)
- Related Node.js processes

### Python Services
- **Demo script** (`demo.py`)
- **Gateway service** (`gateway/main.py`)
- **KMS service** (`kms/main.py`)
- **QKD Simulator** (`qkd_sim/main.py`)
- **Django development server** (`manage.py runserver`)

### Cleanup Actions
- Temporary files (`*.pid`, `*.lock`, `nohup.out`)
- Cache directories (`__pycache__`, `.next`, `node_modules/.cache`)
- Log files (optional)

## ⚠️ Emergency Stop Scripts

Use emergency scripts only when normal scripts fail or in critical situations.

**⚠️ Warning:** Emergency scripts use force-kill methods and may not allow graceful shutdown.

### When to Use Emergency Scripts:
- Normal stop scripts hang or fail
- Processes are unresponsive
- System resources are critically low
- Immediate termination required

### Emergency Script Actions:
- **Immediate process termination** (no graceful shutdown)
- **Docker force-stop** all containers
- **System-wide process cleanup** (requires sudo on Linux)

## 🔧 Troubleshooting

### Common Issues

**1. Permission Denied**
```bash
# Linux/macOS: Make scripts executable
chmod +x stop.sh emergency-stop.sh

# Windows: Run as Administrator if needed
```

**2. Python Dependencies Missing**
```bash
# Install required dependencies
pip install psutil

# Or install all requirements
pip install -r requirements.txt
```

**3. Docker Commands Fail**
```bash
# Check Docker daemon status
docker --version
docker-compose --version

# Start Docker if needed
sudo systemctl start docker    # Linux
```

**4. Processes Still Running After Stop**
```bash
# Use emergency stop
./emergency-stop.sh            # Linux/macOS
emergency-stop.bat             # Windows

# Or manually check and kill
python3 stop.py --list         # List remaining processes
```

### Process Verification

**Check remaining processes:**
```bash
# Using Python script
python3 stop.py --list

# Manual checks
ps aux | grep -E "(electron|node|python)" | grep -E "(quieo|quantum|ui-app)"
docker ps -a
```

## 📊 Status Codes

All scripts provide clear status reporting:

- ✅ **Success**: Service stopped successfully  
- ⚠️ **Warning**: Service may still be running or not found
- ❌ **Error**: Failed to stop service
- ℹ️ **Info**: Status information

## 🛡️ Safety Features

### Graceful Shutdown Priority
1. **SIGTERM** (graceful termination request)
2. **Wait period** (allow clean shutdown)
3. **SIGKILL** (force termination as last resort)

### Process Identification Safety
- **Keyword matching** prevents stopping unrelated processes
- **PID verification** ensures accurate targeting
- **Access control** respects system permissions

## 🔄 Integration with Other Scripts

Stop scripts integrate with other quieo management tools:

```bash
# Complete workflow
./quickstart.sh                   # Start all services
python3 demo.py --launch-ui       # Run demo with UI
./stop.sh                         # Stop all services

# Development workflow  
./setup.sh                        # Install dependencies
cd ui-app && npm run dev          # Start UI development
./stop.sh --docker-only          # Stop only backend services
```

## 📞 Support

If stop scripts fail to terminate services:

1. **Try emergency scripts** first
2. **Check process list** with `python3 stop.py --list`
3. **Manual cleanup** if needed:
   ```bash
   # Force kill specific processes
   sudo pkill -f "process_name"
   
   # Docker cleanup
   docker system prune --force
   ```
4. **System restart** as last resort

---

**💡 Pro Tip:** Always use the Python stop script (`stop.py`) for the most reliable cross-platform experience with comprehensive process detection and graceful shutdown capabilities.