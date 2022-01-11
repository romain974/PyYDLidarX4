# PyYDLidarX4
Python 3 binding for YDLidar X4

This is a fork of PyLidar3: https://github.com/lakshmanmallidi/PyLidar3
The original Lib support only an angle resolution of 1° - this fork allow to get 0.1°
new argument:  step_angle = factor for dividing angles (10: 1 value each 0.1°,2: 1 value each 0.5°)

=> Pull request asked to PyLidar3

# Dependencies
pyserial
time
math
enum

# Usage
This package consists of multiple classes representing the version of lidar you are using. The class structure is YdLidarX4 where X4 is version name ydlidar. 

Class structure:
YdLidarX4
Arguments: port, chunk_size(default:6000), step_angle (10: 1 value each 0.1°,2: 1 value each 0.5°).

port: serial port to which device is connected. Example: com4, /dev/ttyAMC0.

chunk_size: Number of bytes of data read from device. Increase in chunk_size results in more averaged angle:distance pairs but increase response time result in slower data acquisition. For faster data acquisition decrease chunk_size.

Note: Calibrate chunk size depends on your application and frequency of device. 
if the chunk size is not enough not all angles are covered. 
Connect -- Begin serial connection with Lidar by opening serial port. Return success status True/False.

StartScanning -- Begin the lidar and returns a generator which returns a dictionary consisting angle(degrees) and distance(millimeters).
Return Format : {angle(0):distance, angle(2):distance,....................,angle(359):distance}

StopScanning -- Stops scanning but keeps serial connection alive.

GetHealthStatus -- Returns True if Health of lidar is good else returns False

GetDeviceInfo -- Returns Information of Lidar version, serial number etc.

Reset -- Reboot the lidar

Disconnect -- Stop scanning and close serial communication with Lidar.
