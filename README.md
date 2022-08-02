# balena-hyperpixel4-square
Minimal example of using [Pimoroni HyperPixel 4.0 Square Touch Display](https://shop.pimoroni.com/products/hyperpixel-4-square?variant=30138251444307) with touch on balena.

### Usage
For starters, please note how this display operates per https://github.com/pimoroni/hyperpixel4/issues/151#issuecomment-907754480:

"The screen doesn't have an SPI data interface or anything befitting basic init and usage from Python. It either runs over DPI driven by the Raspberry Pi's GPIO or - for all intents and purposes - it doesn't run at all. The speed and timing requirements for generating a DPI signal are pretty far outside the grasp of Python.

That said if you let the Pi handle the display- you can just use any Python [or other language] GUI methods to display images on it. This can be anything from PIL running in X and using the "display()" method on an image (if memory serves) or using fullscreen pygame..."

For our example, we'll "let the Pi handle the display" by using the balena [browser block](https://github.com/balenablocks/browser) which has its own X Window server built in. Using the docker-compose here in this repo gives you a customizable browser that displays on the Hyperpixel with touch screen support (assuming you make all of the settings below.)

To extend this example, you could include a web server service that runs a web application, or you could point the default page of the browser block to a publicly-accessible app. Alternatively, you could provide your own display service (like [this](https://hub.balena.io/organizations/balenablocks/blocks/xserver)) and create your own GUI using Python, etc...

### Device configuration

You'll need to set a few [device configuration variables](https://www.balena.io/docs/learn/manage/configuration/) before the display will work. (these are for the HyperPixel Square display only)

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

After you enter these values, your containers will restart and soon your device should start displaying a web page. The browser block has many configuration settings such as kiosk mode that may be appropriate. See them [here](https://github.com/balenablocks/browser#environment-variables)

A few things to note about the HyperPixel display: Due to the way it interacts with the serial port, the device may not boot in development mode when attached to the display. In addition, the HyperPixel uses "basically all" of the GPIO pins, making them unavailable for HATs or other uses. There is however an alternate I2C interface on the back of the HyperPixel.

### Touch screen settings

The touch input may be inverted from the actual display on the creen. To fix this, set the following device variables on the browser block:

`ROTATE_DISPLAY` value = `inverted`

`TOUCHSCREEN` value = `generic ft5x06 (11)`

If you are not using the browser block, you'll need to find the equivalent commands for your windowing system.



