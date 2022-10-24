# Installing Bluetooth
```
apt install bluetooth libbluetooth-dev
pip3 install pybluez
```


# Updating Reticulum
```
wget -P /usr/local/lib/python3.9/dist-packages/RNS https://raw.githubusercontent.com/SebastianObi/Reticulum/master/RNS/Reticulum.py
wget -P /usr/local/lib/python3.9/dist-packages/RNS/Interfaces https://raw.githubusercontent.com/SebastianObi/Reticulum/master/RNS/Interfaces/RNodeBTInterface.py
```

# Installing default Firmware
```
rnodeconf -a
```

# Download new Firmware
```
cd update

wget https://github.com/SebastianObi/RNode_Firmware/raw/master/Release/rnode_firmware_latest_esp32_generic.zip
wget https://github.com/SebastianObi/RNode_Firmware/raw/master/Release/rnode_firmware_latest_featheresp32.zip
wget https://github.com/SebastianObi/RNode_Firmware/raw/master/Release/rnode_firmware_latest_heltec32v2.zip
wget https://github.com/SebastianObi/RNode_Firmware/raw/master/Release/rnode_firmware_latest_lora32v20.zip
wget https://github.com/SebastianObi/RNode_Firmware/raw/master/Release/rnode_firmware_latest_lora32v20_extled.zip
wget https://github.com/SebastianObi/RNode_Firmware/raw/master/Release/rnode_firmware_latest_lora32v21.zip
wget https://github.com/SebastianObi/RNode_Firmware/raw/master/Release/rnode_firmware_latest_lora32v21_extled.zip
wget https://github.com/SebastianObi/RNode_Firmware/raw/master/Release/rnode_firmware_latest_tbeam.zip

unzip rnode_firmware_latest_esp32_generic.zip
unzip rnode_firmware_latest_featheresp32.zip
unzip rnode_firmware_latest_heltec32v2.zip
unzip rnode_firmware_latest_lora32v20.zip
unzip rnode_firmware_latest_lora32v20_extled.zip
unzip rnode_firmware_latest_lora32v21.zip
unzip rnode_firmware_latest_lora32v21_extled.zip
unzip rnode_firmware_latest_tbeam.zip

cd ..
```

# Update Firmware
```
rnodeconf -u
```


# Finished


# Bluetooth device scan
```
pi@RPi3:~ $ bluetoothctl
    [bluetooth]# set-scan-filter-clear
    SetDiscoveryFilter success
    [bluetooth]# scan on
    Discovery started
[CHG] Controller E4:5F:01:D3:02:D1 Discovering: yes
[NEW] Device 30:83:98:DC:CA:22 RNodeBT
[bluetooth]# exit
```

# Reticulum config:
```
#RNodeBT LoRa Interface
[[RNodeBT LoRa Interface]]
type = RNodeBTInterface
enabled = True
outgoing = True
device_addr = 30:83:98:DC:CA:22
frequency = 867200000
bandwidth = 125000
txpower = 7
spreadingfactor = 8
codingrate = 5
##id_callsign = MYCALL-0
##id_interval = 600
flow_control = False
```

# Reticulum start:
```
root@raspberrypi:~# rnsd
[2022-10-23 16:35:05] [Notice] Searching Bluetooth device 30:83:98:DC:CA:22...
[2022-10-23 16:35:05] [Notice] Connecting to Bluetooth device 'ESP32SPP' on 30:83:98:DC:CA:22, port 1...
[2022-10-23 16:35:08] [Notice] Bluetooth device 30:83:98:DC:CA:22 is now connected
[2022-10-23 16:35:08] [Notice] RNodeBTInterface[RNodeBT LoRa Interface] is configured and powered up
[2022-10-23 16:35:08] [Notice] Started rnsd version 0.3.17
```

# Reticulum status:

```
raspberrypi:~# rnstatus

 Shared Instance[37428]
    Status  : Up
    Serving : 0 programs
    Rate    : 1.00 Gbps
    Traffic : 0 B↑
              0 B↓

 TCPInterface[RNS Testnet Dublin/dublin.connect.reticulum.network:4965]
    Status  : Up
    Mode    : Full
    Rate    : 10.00 Mbps
    Traffic : 395 B↑
              195 B↓

 RNodeBTInterface[RNodeBT LoRa Interface]
    Status  : Up
    Mode    : Full
    Rate    : 3.12 kbps
    Traffic : 195 B↑
              179 B↓

 Reticulum Transport Instance <96a2bdfbb5566dda11516bb0a4121af6> is running
```