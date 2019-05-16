# MakeCode Extension for ESP8266 Wifi Modules and ThingSpeak

This extension/package is a modified version from [elecfreaks/pxt-esp8266iot](https://github.com/elecfreaks/pxt-esp8266iot).

You need a account and a channel on [ThingSpeak](https://thingspeak.com/) to get the write API key.

![pctdetail 775-090 1](https://user-images.githubusercontent.com/44191076/50425186-76ada780-08ac-11e9-956c-9ebd6be09bb2.jpg)
![esp8266-pinout](https://user-images.githubusercontent.com/44191076/50428909-fc097a00-08f5-11e9-91f1-921d1b957f29.png)
![esp8266_bb](https://user-images.githubusercontent.com/44191076/50541952-e513a200-0beb-11e9-9820-05f6798b2044.png)

Connect VCC and CH to 3.3V (sufficint power needed; the power from micro:bit's USB cable is NOT ENOUGH), GND to GND, RX and TX to two I/O pins, ignore the rest. See [here](https://components101.com/wireless/esp8266-pinout-configuration-features-datasheet) for more details.

## License

MIT

## Supported targets

* for PXT/microbit
