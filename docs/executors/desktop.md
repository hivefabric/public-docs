# Desktop Executors

Desktop executors run on Windows, Linux, and macOS machines.

## Installation

### Linux

```bash
# Install from package manager or binary
curl -O https://releases.hive.io/executor/linux/hive-executor
chmod +x hive-executor
./hive-executor --install
```

### Windows

Download installer from https://releases.hive.io/executor/windows/

### macOS

```bash
brew install hive-executor
hive-executor --install
```

## Configuration

```yaml
# ~/.hive/config.yml
node_id: "desktop-1"
platform: "linux"
max_concurrent_tasks: 4
resources:
  cpu_cores: 4
  memory_gb: 16
  storage_gb: 100
actions:
  - name: "file_process"
    enabled: true
  - name: "compile"
    enabled: true
```

## Capabilities Advertisement

Executors auto-detect:
- OS and architecture
- Available CPU cores
- Disk space
- Network connectivity
- Installed runtimes (Python, Node.js, etc.)

## Task Execution

Tasks execute in isolated containers or VMs:

```yaml
nodes:
  - id: "compute"
    type: "step"
    action: "run_script"
    params:
      script: "process_data.py"
      timeout: 3600
```

## Monitoring

```bash
hive-executor status
hive-executor logs --follow
```
