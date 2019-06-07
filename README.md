# MakeCode Extension for ESP8266 Wifi Modules and ThingSpeak IoT Platform

![pctdetail 775-090 1](https://user-images.githubusercontent.com/44191076/50425186-76ada780-08ac-11e9-956c-9ebd6be09bb2.jpg)
![92153_wm_logo](https://user-images.githubusercontent.com/44191076/58067910-d68d4d80-7bc1-11e9-9ea8-5605837dd5d5.png)

This extension/package is heavily modified from [elecfreaks/pxt-esp8266iot](https://github.com/elecfreaks/pxt-esp8266iot), also derived from [my first modification](https://github.com/alankrantas/pxt-esp8266iot) and my [micro:bit web server project](https://www.hackster.io/alankrantas/wifi-web-server-on-bbc-micro-bit-and-esp-01-esp8266-498e0d). This version has less blocks and checks the AT responses whenever the ESP8266 tries to connect Wifi, ThingSpeak as well as uplolding data.

This extension is primary targeted for ESP-01/ESP-01S or similar [ESP8266](https://github.com/esp8266/esp8266-wiki/wiki) Wifi modules loaded with factory firmware, so that you can make ThingSpeak IoT projects on [BBC micro:bits](https://microbit.org/).

You need a account and a channel on [ThingSpeak](https://thingspeak.com/) to get the write API key. Please do not share your Wifi and API info online.

## Wiring

![esp8266-pinout](https://user-images.githubusercontent.com/44191076/50428909-fc097a00-08f5-11e9-91f1-921d1b957f29.png)

Connect VCC and CH to 3.3V (sufficint power needed, about 200-400 mA at least; the power from micro:bit's USB port alone is NOT ENOUGH), GND to GND, TX (transmit) and RX (receive) to two I/O pins, ignore the rest. See [here](https://components101.com/wireless/esp8266-pinout-configuration-features-datasheet) for more details. Sometimes you might also need to unplug and re-plug power to start up the ESP8266 properly.

You can also add a USB-to-TTL module to read full AT responses from your ESP8266 via terminal software on your computer: (The LED in the circuit is not needed)

![microbit_esp8266_ArNB60xdJd](https://user-images.githubusercontent.com/44191076/57862847-9c235980-782b-11e9-9588-3e7fe76342ee.png)

Noted that the Tx and Rx in the picture above represents the reassigned serial port pins of micro:bit:

* Tx of micro:bit -> Rx of ESP8266
* Rx of micro:bit -> Tx of ESP8266

## Sample Code

Use initialize block to connect to your Wifi router, and use upload block to update data to your channel on ThingSpeak.

If it failed to connect to Wifi in the first place, the update block would do nothing. If the update block failed to connect to ThingSpeak first, it would not send the data. You can use other blocks to check the status.

Is is also recommended to wait several seconds between each update. Not every connect or update attempt would be successful on ThingSpeak.

![microbit-screenshot](https://user-images.githubusercontent.com/44191076/58189752-a642cd80-7ced-11e9-8557-3be87aa795fa.png)

```blocks
ESP8266_ThingSpeak.connectWifi(
SerialPin.P0,
SerialPin.P1,
BaudRate.BaudRate115200,
"your_ssid",
"your_pw"
)
basic.forever(function () {
    ESP8266_ThingSpeak.connectThingSpeak(
    "api.thingspeak.com",
    "your_write_api_key",
    0,
    0,
    0,
    0,
    0,
    0,
    0,
    0
    )
    ESP8266_ThingSpeak.wait(5000)
})
```

In the pic below is the test result of uploading analog readings of MQ7/MQ2 sensors.

![1](https://user-images.githubusercontent.com/44191076/57868088-e52bdb80-7834-11e9-8c8a-29c5932cd8ab.jpg)

## License

MIT

## Supported targets

* for PXT/microbit
