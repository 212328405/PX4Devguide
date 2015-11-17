# PX4 System Console

The system console allows low-level access to the system, debug output and analysis of the system boot process. The most convient way to connect it is by using a [Dronecode probe](http://nicadrone.com/index.php?id_product=65&controller=product), but a plain FTDI cable can be used as well.

## Wiring the Console

The system console can be accessed through the Dronecode probe or an FTDI cable. Both options are explained in the section below.

### Connecting via Dronecode Probe

Connect the 6-pos DF13 1:1 cable on the [Dronecode probe](http://nicadrone.com/index.php?id_product=65&controller=product) to the SERIAL4/5 port of Pixhawk.

![](images/console/dronecode_probe.jpg)

### Connecting via FTDI 3.3V Cable

If no Dronecode probe is at hand an FTDI 3.3V (Digi-Key: [768-1015-ND](http://www.digikey.com/product-detail/en/TTL-232R-3V3/768-1015-ND/1836393)) will do as well.

| Pixhawk  |         | FTDI    |        |
| -- | -- | -- | -- |
|1         | +5V (red)     |         | N/C    |
|2         | S4 Tx      | 5       | N/C   |
|3         | S4 Rx      | 4       | N/C   |
|4         | S5 Tx      | 5       | FTDI Rx (yellow)   |
|5         | S5 Rx      | 4       | FTDI TX (orange)   |
|6         | GND     | 1       | FTDI GND (black)   |

The connector pinout is shown in the figure below.

![](images/console/console_connector.jpg)

The complete wiring is shown below.

![](images/console/console_debug.jpg)

## Opening the Console

After the console connection is wired up, use the default serial port tool of your choice or the defaults described below:

### Linux / Mac OS: Screen

Install screen on Ubuntu (Mac OS already has it installed):

<div class="host-code"></div>

```bash
sudo apt-get install screen
```

Connect screen at 57600 baud, 8 data bits, 1 stop bit to the right serial port (use `ls /dev/tty*` and watch what changes when unplugging / replugging the USB device). Common names are `/dev/ttyUSB0` and `/dev/ttyACM0` for Linux and `/dev/tty.usbserial-ABCBD` for Mac OS.

<div class="host-code"></div>

```bash
screen /dev/ttyXXX 57600 8N1
```

### Windows: PuTTY

Download [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) and start it.

Then select 'serial connection' and set the port parameters to:

  * 57600 baud
  * 8 data bits
  * 1 stop bit

## Getting Started on the Console

Type `ls` to view the local file system, type `free` to see the remaining free RAM. The console will also display the system boot log when power-cycling the board.

```bash
nsh> ls
nsh> free
```
