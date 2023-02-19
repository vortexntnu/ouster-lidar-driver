# Ouster Lidar Driver
The code in this repository is a fork of the official ouster lidar example code, but stripped down to that which is required for the ROS driver to run.

Run the ROS driver using the following command:

```
roslaunch ouster_ros ouster.launch sensor_hostname:=<sensor-ip> metadata:=<filename>
```

where

* **sensor-ip**: Either a numeric ip or a fixed .local ip, which may look like `10.0.0.50` and `os1-122007000043.local` respectively.

# Notes
To run the driver, the host machine must be on the same subnet as the lidar. You can easily verify this by running

```
ping <sensor-ip>
```

and see that you get a response. The sensor ip can be resolved in two ways, assuming a DHCP server is providing an address to the sensor. The first (and likely easiest) is to use the model and serial number of the sensor. For example, an Ouster OS1 lidar with the serial number `122001000011` can be found on the address `os1-122001000011.local`. The other way is to use a network discovery tool such as nmap to find the ip that the sensor has been assigned. For this method, disconnect the lidar, then run `nmap -sP XXX.XXX.XXX.0/24` where the X's need to be replaced with the network you are on. This should give you a list of active clients. Then connect the sensor and rerun the command. You should now see one new client, and the ip of this new client will be the ip of the lidar.

The lidar may jank up sometimes and not respond to the .local address, in which case you may want to power cycle the sensor.