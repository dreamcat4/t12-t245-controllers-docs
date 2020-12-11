# K-Type Thermocouple

<!-- MarkdownTOC -->

* [K-Type Thermocouple](#k-type-thermocouple)
* [MAX6675 K type thermocouple module](#max6675-k-type-thermocouple-module)
	* [Usage](#usage)

<!-- /MarkdownTOC -->

<a id="k-type-thermocouple"></a>
# K-Type Thermocouple

A k-type thermocouple is useful for calibrating your soldering iron tip. And investigating what is happening with the thermocouple in the tip. For example for adding an unsupported handle. Or to check the temperature is accurate.

Very often these newer KSGER or "T12 OLED" pcb will come with a poor quality op-amp (aka "comparator"). The op-amp is responsible for amplifiying the signal from the thermocouple in the tip. And then passes the signal onto the ADC input of the MCU.  The op-amp requires a high gain, needs good performance.  If it's cheap component (such as unknown with package marking "61LJV") or fake (not genuine, has correct package marking, but is a clone / not authentic) then the temperature may be far off. Or jump around.

By using am external k-type thermocouple you can then check whether your op-amp needs replacing. Or otherwise research and document other behaviour specific to the tip's own embedded thermocouple.


<a id="max6675-k-type-thermocouple-module"></a>
# MAX6675 K type thermocouple module

This module communicates over SPI bus. Therefore it requires an arduino (or whatever your favorite MCU that can talk SPI protocol. So that you can receive the temperature data output from the module.

This module can be found as a kit (along with a k-type thermocouple included!) on Aliexpress. Just search for "MAX6675", for example:

* https://www.aliexpress.com/item/32682640169.html (listing may expire)


<a id="usage"></a>
## Usage

A really detailed and helpful guide here. It tells everything about the MAX6675, and how to use it:

* https://www.best-microcontroller-projects.com/max6675.html ([Mirror](https://htmlpreview.github.io/?https://github.com/dreamcat4/t12-t245-controllers-docs/blob/master/tools/k-type%20thermocouple/MAX6675%20Simple%20Arduino%20Tutorial%20for%20measuring%20up%20to%201024C%20(2020-06-16%2012_27_51).html))

There are also many other guides on the internet.




