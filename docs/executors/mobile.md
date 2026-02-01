# Mobile Executors

Mobile executors allow Hive tasks to run on Android and iOS devices.

## Android Executor

### Installation

```bash
# Install via APK or app store
adb install hive-executor.apk
```

### Configuration

```xml
<!-- hive-config.xml -->
<hive>
  <node_id>mobile-1</node_id>
  <platform>android</platform>
  <capabilities>
    <storage_mb>1024</storage_mb>
    <memory_mb>2048</memory_mb>
    <actions>
      <action name="camera_capture"/>
      <action name="sensor_read"/>
      <action name="process_image"/>
    </actions>
  </capabilities>
</hive>
```

## iOS Executor

### Installation

Via App Store or TestFlight. See iOS app documentation.

### Permissions

Request required permissions in task definition:

```yaml
nodes:
  - id: "capture"
    type: "step"
    action: "camera_capture"
    required_permissions:
      - "camera"
      - "location"
```

## Mobile-Specific Patterns

### Sensor Data Collection

```yaml
nodes:
  - id: "read-sensors"
    type: "fork"
    join_strategy: "all"
    children:
      - id: "accelerometer"
        type: "step"
        action: "read_accelerometer"
      - id: "gps"
        type: "step"
        action: "read_gps"
```

### Battery Awareness

Mobile executors honor battery constraints. Tasks may be paused or scheduled during high-battery periods.

## Debugging

Check logs via:
```bash
adb logcat | grep hive
```
