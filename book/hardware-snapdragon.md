# Snapdragon Flight Autopilot

The Snapdragon Flight platform is a high-end autopilot / onboard computer which runs the PX4 Flight Stack on the DSP on the QuRT real time operating system using the [DSPAL API](https://github.com/ATLFlight/dspal) for POSIX compatibility. In comparison to [Pixhawk](hardware-pixhawk.md) it adds a camera and WiFi and high-end processing power, and different IO.

More information about the Snapdragon Flight platform is at [Snapdragon-Flight-Details](https://www.intrinsyc.com/qualcomm-snapdragon-flight-details/)

![](images/hardware/hardware-snapdragon.jpg)

## Quick Summary

  * System-on-Chip: [Snapdragon 801](https://www.qualcomm.com/products/snapdragon/processors/801)
    * CPU: Quad-core 2.26 GHz Krait
    * DSP: Hexagon DSP (QDSP6 V5A) – 801 MHz+256KL2 (running the flight code)
    * GPU: Qualcomm® Adreno™ 330 GPU
    * RAM: 2GB LPDDR3 PoP @931 MHz
  * Storage: 32GB eMMC Flash
  * Video: Sony IMX135 on Liteon Module 12P1BAD11
    * 4k@30fps 3840×2160 video capture to SD card with H.264 @ 100Mbits (1080p/60 with parallel FPV), 720p FPV
  * Optic Flow: Omnivision OV7251 on Sunny Module MD102A-200
    * 640x480 @ 30/60/90 fps
  * Wifi: Qualcomm® VIVE™ 1-stream 802.11n/ac with MU-MIMO † Integrated digital core
  * BT/WiFi: BT 4.0 and 2G/5G WiFi via QCA6234
    * 802.11n, 2×2 MIMO with 2 uCOAX connectors on-board for connection to external antenna
  * GPS: Telit Jupiter SE868 V2 module (use of an external u-Blox module is recommended by PX4 instead)
    * uCOAX connector on-board for connection to external GPS patch antenna 
    * CSR SiRFstarV @ 5Hz via UART
  * Accelerometer / Gyro / Mag: Invensense MPU-9250 9-Axis Sensor, 3x3mm QFN, on bus SPI1
  * Baro: Bosch BMP280 barometric pressure sensor, on bus I2C3
  * Power: 5VDC via external 2S-6S battery regulated down to 5V via APM adapter
  * Availability: [Intrinsyc Store](http://shop.intrinsyc.com/products/snapdragon-flight-dev-kit)

## Connectivity

  * One USB 3.0 OTG port (micro-A/B)
  * Micro SD card slot
  * Gimbal connector (PWB/GND/BLSP)
  * ESC connector (2W UART)
  * I2C
  * 60-pin high speed Samtec QSH-030-01-L-D-A-K expansion connector
    * 2x BLSP ([BAM Low Speed Peripheral](http://www.inforcecomputing.com/public_docs/BLSPs_on_Inforce_6540_6501_Snapdragon_805.pdf))
    * USB

## Pinouts

<aside class="warning">
Although the Snapdragon uses DF13 connectors, the pinout is different from Pixhawk.
</aside>

### WiFi

  * WLAN0, WLAN1 (+BT 4.0): U.FL connector: [Taoglas adhesive antenna (DigiKey)](http://www.digikey.com/product-detail/en/FXP840.07.0055B/931-1222-ND/3877414)

### J9 / GPS

| Pin | Signal | Comment |
| -- | -- | -- |
| 1 | 3.3V | |
| 2 | UART2_TX | Output (3.3V) |
| 3 | UART2_RX | Input (3.3V) |
| 4 | I2C2_SDA | (3.3V) |
| 5 | GND | |
| 6 | I2C2_SCL | (3.3V) |

### J12 / Gimbal bus

| Pin | Signal | Comment |
| -- | -- | -- |
| 1 | 3.3V | |
| 2 | UART8_TX | Output (3.3V) |
| 3 | UART8_RX | Input (3.3V) |
| 4 | APQ_GPIO_47 | (3.3V) |
| 5 | GND | |
| 6 | APQ_GPIO_48 | (3.3V) |

### J13 / ESC bus

| Pin | Signal | Comment |
| -- | -- | -- |
| 1 | 5V | |
| 2 | UART6_TX | Output (5V) |
| 3 | UART6_RX | Input (5V) |
| 4 | APQ_GPIO_29 | (5V) |
| 5 | GND | |
| 6 | APQ_GPIO_30 | (5V) |

### J14 / Power

| Pin | Signal | Comment |
| -- | -- | -- |
| 1 | 5V DC | Power input |
| 2 | GND | |
| 3 | I2C3_SCL | (5V) |
| 4 | I2C3_SDA | (5V) |

### J15 / Radio Receiver / Sensors

| Pin | Signal | Comment |
| -- | -- | -- |
| 1 | 3.3V | |
| 2 | UART9_TX | Output |
| 3 | UART9_RX | Input |
| 4 | I2C9_SDA | |
| 5 | GND | |
| 6 | I2C9_SCL | |

## Dimensions

![](images/hardware/hardware-snapdragon-dimensions.png)

