# balena-hyperpixel4-square
Minimal example of using Pimoroni Hyperpixel4 Square w/touch on balena

### Hardware/Software setup

- [Pimoroni HyperPixel 4.0 Square Touch Display](https://shop.pimoroni.com/products/hyperpixel-4-square?variant=30138251444307) also available [here](https://www.adafruit.com/product/4499) connected to a Pi 3A + in this example (But other Pi versions should work as well)

- BalenaOS 

### Device configuration

You'll need to set a few [device configuration variables](https://www.balena.io/docs/learn/manage/configuration/). (these are for the HyperPixel Square display only)

Edit the "Define DT overlays" variable and set to `"hyperpixel4-square-pi3"` (including the quotes)

Change the "Define device GPU memory in megabytes." value to at least 64

Set the following custom configuration variables:

| Variable Name | Variable Value |
| ------------ | ----------- |
| RESIN_HOST_CONFIG_display_default_lcd | 1 |
| RESIN_HOST_CONFIG_dpi_group | 2 |
| RESIN_HOST_CONFIG_dpi_mode | 87 |
| RESIN_HOST_CONFIG_dpi_output_format | 0x5f026 |
| RESIN_HOST_CONFIG_dpi_timings | 720 0 20 20 40 720 0 15 15 15 0 0 0 60 0 36720000 4 |
| RESIN_HOST_CONFIG_enable_dpi_lcd | 1 |
| RESIN_HOST_CONFIG_framebuffer_height | 720 |
| RESIN_HOST_CONFIG_framebuffer_width | 720 |
| RESIN_HOST_CONFIG_overscan_bottom | 0 |
| RESIN_HOST_CONFIG_overscan_left | 0 |
| RESIN_HOST_CONFIG_overscan_right | 0 |
| RESIN_HOST_CONFIG_overscan_top | 0 |

After you enter these values, your containers will restart and soon your device should start displaying any images (if available.)

A few things to note about the HyperPixel display: Due to the way it interacts with the serial port, the device may not boot in development mode when attached to the display. In addition, the HyperPixel uses "basically all" of the GPIO pins, making them unavailable for HATs or other uses. There is however an alternate I2C interface on the back of the HyperPixel.
