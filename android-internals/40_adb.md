# Android Debug Bridge

### Location
```
~/Android/Sdk/platform-tools/adb
```

### Adb is a server-client application
- A client, which sends commands. The client runs on your development machine. 
- A daemon (adbd), which runs commands on a device. 
The daemon runs as a background process on each device.
- A server, which manages communication between the client and the daemon. 
The server runs as a background process on your development machine.
The port is 5037


### Enable USB debugging on your device


# ADB commands

### Show all devices
```
adb devices
```

### Show all devices with additional info
### this outputs the 'serial numbers' of available devices and emulators
```
adb devices -l
```

### Send commands to specific device
### indicate the serial number with '-s'
### or set the env variable $ANDROID_SERIAL
```
adb -s emulator-5554 install HelloWorld.apk
```






### 'emulator' command
### location:
```
~/Android/Sdk/tools/emulator
```

### Show available emulators
```
emulator -list-avds
```









