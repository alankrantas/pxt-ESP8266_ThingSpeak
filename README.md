# MakeCode Extension for ESP8266 Wifi Modules and ThingSpeak IoT Platform

![pctdetail 775-090 1](https://user-images.githubusercontent.com/44191076/50425186-76ada780-08ac-11e9-956c-9ebd6be09bb2.jpg)
![92153_wm_logo](https://user-images.githubusercontent.com/44191076/58067910-d68d4d80-7bc1-11e9-9ea8-5605837dd5d5.png)

This extension/package is heavily modified from [elecfreaks/pxt-esp8266iot](https://github.com/elecfreaks/pxt-esp8266iot), also derived from [my first modification](https://github.com/alankrantas/pxt-esp8266iot) and my [micro:bit web server project](https://www.hackster.io/alankrantas/wifi-web-server-on-bbc-micro-bit-and-esp-01-esp8266-498e0d). This version has less blocks and checks the AT responses whenever the ESP8266 tries to connect Wifi, ThingSpeak as well as uplolding data.

This extension is primary targeted for ESP-01/ESP-01S or similar [ESP8266](https://github.com/esp8266/esp8266-wiki/wiki) Wifi modules loaded with factory firmware, so that you can make ThingSpeak IoT projects on [BBC micro:bits](https://microbit.org/).

You need a account and a channel on [ThingSpeak](https://thingspeak.com/) to get the write API key. Please do not share your Wifi and API info online.

# Note to Users

This extension/driver is designed for **AI-Thinker ESP-01/ESP-01S** ESP8266 boards with their (older) default AT firmwares, which are dated from around 2014-2016. I have tested it with regular ESP8266 boards flashed with up-to-date AT firmwares, and it works to some extent. 

To be honest, using an external WiFi chip with micro:bit is not an elegent solution. There's simply too many factors can go wrong in both hardware and software. The only way to see what's wrong is using an USB-to-TTL cable or module (most of the products should work) to read the AT responses directly from your computer.

Please beware that this is more like an experiment to bring IoT project to micro:bit, and very possibly outdated/unusable for more recent products. I would say using a ESP8266 (NodeMCU or D1 mini, etc) with standard MicroPython would be a easier choice to make IoT projects.

Now, some common questions people sent me:

Q: <i>Why it didn't work? Can you help me????? I need this for my own project!!!!!</i>

A: Unless I have the same hardware as you and you had copied the AT responses (which people never did) so that I can tell what's wrong, I don't have time to guess every single one of the possibility. And please, don't try to trick me/hint that I should do free work for you ASAP.

Q: <i>Can you modify the code so that I can ___ ?</i>

A: This extension is for everyone and might be currently used by some people. I won't modify it for your own purpose unless you have found serious bugs that I can confirm/repeat and fix. You are welcome to fork it and modify it yourself though. You can import your own extension with its Github URL in the MakeCode editor.

Q: <i>Can you modify the code so that I can receive data from ThinkSpeak or somewhere?</i>

A: No, because receiving and parsing incoming raw HTTP data would be more diffcult and messy to implement with MakeCode blocks. Again, it would be far more easier to use regular ESP8266 boards with MicroPython.

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
