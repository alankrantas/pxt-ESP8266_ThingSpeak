# MakeCode Extension for ESP8266 Wifi Modules and ThingSpeak

This extension/package is modified from [elecfreaks/pxt-esp8266iot](https://github.com/elecfreaks/pxt-esp8266iot), also derived from [my first modification](https://github.com/alankrantas/pxt-esp8266iot). I changed the name so people can use it along with Elecfreaks' other extensions.

This version also has less blocks and checks the AT responses when the ESP8266 tries to connect Wifi, ThingSpeak as well as uplolding data.

You need a account and a channel on [ThingSpeak](https://thingspeak.com/) to get the write API key. Please do not share your Wifi and API info online.

![pctdetail 775-090 1](https://user-images.githubusercontent.com/44191076/50425186-76ada780-08ac-11e9-956c-9ebd6be09bb2.jpg)
![esp8266-pinout](https://user-images.githubusercontent.com/44191076/50428909-fc097a00-08f5-11e9-91f1-921d1b957f29.png)
![esp8266_bb](https://user-images.githubusercontent.com/44191076/50541952-e513a200-0beb-11e9-9820-05f6798b2044.png)

Connect VCC and CH to 3.3V (sufficint power needed; the power from micro:bit's USB cable is NOT ENOUGH), GND to GND, RX and TX to two I/O pins, ignore the rest. See [here](https://components101.com/wireless/esp8266-pinout-configuration-features-datasheet) for more details.

You can also use a USB-to-TTL module to read AT responses from your ESP8266:

![microbit_esp8266_ArNB60xdJd](https://user-images.githubusercontent.com/44191076/57862847-9c235980-782b-11e9-9588-3e7fe76342ee.png)

## Sample Code

Use initialize block to connect to your Wifi router, and use upload block to update data to your channel on ThingSpeak.

If it failed to connect to Wifi, the update block would do nothing. If the update block failed to connect to ThingSpeak, it would not send the data.

Is is recommended to wait several seconds between each update. It's normal that not every update attempt will be successful.

![microbit-screenshot](https://user-images.githubusercontent.com/44191076/57862632-42bb2a80-782b-11e9-8031-05145d642791.png)

```
ESP8266_ThingSpeak.initialize_wifi(
SerialPin.P0,
SerialPin.P1,
BaudRate.BaudRate115200,
"your_ssid",
"your_pw"
)
basic.forever(function () {
    ESP8266_ThingSpeak.connect_thingspeak(
    "api.thingspeak.com",
    "your_API_key",
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

## License

MIT

## Supported targets

* for PXT/microbit
