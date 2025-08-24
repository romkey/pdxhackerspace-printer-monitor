# Prusa Printer Monitor Blueprint

A Home Assistant blueprint for monitoring Prusa printers and sending notifications to Slack with optional photo integration.

## Features

- **State Change Monitoring**: Automatically detects when your printer changes states (printing, paused, completed, failed, etc.)
- **Periodic Status Updates**: Sends status updates every 15 minutes (configurable) while actively printing
- **Slack Integration**: Sends rich notifications to Slack with emojis and formatted messages
- **Photo Integration**: Optionally includes photos from ESPHome cameras in notifications
- **Temperature Monitoring**: Includes temperature data from ESPHome sensors (if available)
- **Spam Prevention**: Configurable timeout to prevent spam notifications when printer briefly becomes unavailable
- **Flexible Configuration**: Works with or without optional sensors/cameras

## Prerequisites

1. **PrusaLink Integration**: Your Prusa printer must be set up with the PrusaLink integration in Home Assistant
2. **Slack Integration**: The Slack integration must be configured in Home Assistant
3. **ESPHome Sensors** (Optional): If you have ESPHome-based sensors for temperature and camera

## Installation

1. Copy the `prusa_printer_monitor.yaml` file to your Home Assistant configuration directory
2. In Home Assistant, go to **Settings** → **Blueprints**
3. Click **Import Blueprint** and select the YAML file
4. Click **Use Blueprint** to create a new automation

## Configuration

### Required Inputs

- **Prusa Printer Entity**: Select your printer entity from the PrusaLink integration
- **Slack Notification Service**: Choose your Slack notification service (default: `notify.slack`)

### Optional Inputs

- **Camera Entity**: Select your ESPHome camera entity for photo attachments
- **Temperature Sensor**: Select your ESPHome temperature sensor entity
- **Status Update Interval**: How often to send status updates during printing (default: 15 minutes)
- **Unavailable Timeout**: How long to wait before considering printer unavailable (default: 30 seconds)
- **Enable Photo Attachments**: Toggle photo attachments on/off (default: true)

## Notification Types

### State Change Notifications

- **🖨️ Print Started**: When a new print job begins
- **✅ Print Completed**: When a print job finishes successfully
- **❌ Print Failed**: When a print job fails
- **⏸️ Print Paused**: When a print job is paused
- **▶️ Print Resumed**: When a paused print job resumes
- **🔄 Printer State Changed**: For any other state changes
- **🖨️ Printer Unavailable**: When printer is unavailable for extended period

### Periodic Updates

- **📊 Print Status Update**: Sent every 15 minutes (configurable) while printing, including:
  - Current progress percentage
  - Time remaining
  - Print duration
  - Temperature (if sensor available)
  - Current photo (if camera available)

## Message Format

All notifications include:
- Printer name
- Current file being printed (if applicable)
- Progress percentage (if applicable)
- Timestamp
- Relevant status information
- Optional photo attachment

## Example Notifications

### Print Started
```
🖨️ Print Started

A new print job has started!

**Printer:** Prusa i3 MK3S+
**File:** calibration_cube.gcode
**Progress:** 0%
**Time:** 2024-01-15 14:30:25
```

### Status Update
```
📊 Print Status Update

**Printer:** Prusa i3 MK3S+
**File:** calibration_cube.gcode
**Progress:** 45%
**Time Remaining:** 1h 23m
**Print Duration:** 2h 15m
**Temperature:** 23.5°C
**Time:** 2024-01-15 16:45:30
```

### Print Completed
```
✅ Print Completed

Print job completed successfully!

**Printer:** Prusa i3 MK3S+
**File:** calibration_cube.gcode
**Duration:** 4h 32m
**Time:** 2024-01-15 19:02:45
```

## Troubleshooting

### Printer Shows as Unavailable
- Check your PrusaLink connection
- Verify the printer is powered on and connected to the network
- The blueprint includes a configurable timeout to prevent spam notifications

### Photos Not Appearing
- Ensure your camera entity is properly configured
- Check that the camera has an `entity_picture` attribute
- Verify the `enable_photos` option is set to true

### Temperature Not Showing
- Make sure your temperature sensor entity is selected
- Verify the sensor is reporting valid temperature values

### Slack Notifications Not Working
- Check your Slack integration configuration
- Verify the notification service name is correct
- Test the notification service manually

## Customization

You can modify the blueprint to:
- Add additional notification channels (Discord, Telegram, etc.)
- Include more sensor data (humidity, air quality, etc.)
- Change notification frequency
- Add custom message formatting
- Include additional printer attributes

## Support

For issues or questions:
1. Check the Home Assistant logs for error messages
2. Verify all entity names and service names are correct
3. Test individual components manually before using the blueprint

## License

This blueprint is provided as-is for educational and personal use.
