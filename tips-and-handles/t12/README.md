# T12 Handles

<!-- MarkdownTOC -->

* [Circuit](#circuit)
* [Tip](#tip)
* [Thermocouple](#thermocouple)
* [GX12-5 Pin Connector](#gx12-5-pin-connector)
* [NTC Thermistor & SW-200D Tilt Switch](#ntc-thermistor--sw-200d-tilt-switch)
* [KSGER Aluminium Handle](#ksger-aluminium-handle)
  * [Wiring in the handle](#wiring-in-the-handle)

<!-- /MarkdownTOC -->

<a id="circuit"></a>
## Circuit

![T12 Circuit](t12-wiring-circuit.jpg)

<a id="tip"></a>
## Tip

![Wiring - T12 Tip](t12-bit.png)

<a id="thermocouple"></a>
## Thermocouple

The T12 thermocouple is oddball metallurgy, measured empirically in Hakko Patent US6087631A for the look up table, 20-21uV/°C accurate from 200°-600°C.

<a id="gx12-5-pin-connector"></a>
## GX12-5 Pin Connector

![GX12 5 Pin Connector](ksger-wiring-gx12-5pin.jpg)

<a id="ntc-thermistor--sw-200d-tilt-switch"></a>
## NTC Thermistor & SW-200D Tilt Switch

![Thermistor and Tilt Switch](thermistor-and-tilt-switch.jpg)

* Datasheet for SW-200D Tilt switch - https://raw.githubusercontent.com/SeeedDocument/Grove-Tilt_Switch/master/res/SW200D_datasheet.pdf

<a id="ksger-aluminium-handle"></a>
## KSGER Aluminium Handle

* Purchase Link: https://www.aliexpress.com/item/33004762167.html

![KSGER T12 Aluminium Handle](ksger-aluminum-handle.jpg)

<a id="wiring-in-the-handle"></a>
### Wiring in the handle

|GX12 Pin|Wire Color|T12 Pin|Function|
|--------|----------|-------|--------|
|1       |Blue      |       |SW-200D Tilt switch, then to Ground (Green wire)|
|2       |White     |       |NTC Thermistor (unknown, 104?, looks like 102PS1J?), then to - (Black wire) |
|3       |Green     |E      |Tip Ground|
|4       |Black     |-      |Heater Negative|
|5       |Red       |+      |Heater Positive|

![Wiring - Top View](ksger-aluminum-handle_wiring-top-view.jpg)





