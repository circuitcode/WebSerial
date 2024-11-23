# WebSerial

WebSerial is a project that allows communication with serial devices directly from the web browser using the Web Serial API.

## Features

- Communicate with serial devices from the browser
- Easy-to-use API
- Cross-platform support
- Uses AsyncTCP / ESPAsyncWebServer for ESP32

## Build web interface

Install frontend dependencies:

```bash
yarn && yarn build
```

## Implementation

### Add WebSerial to your platformIO project platformio.ini

```ini
[env:esp32]
platform = espressif32
board = esp32dev
framework = arduino
monitor_speed = 115200
lib_deps =
    WebSerial
```

### Include the library in your code

```cpp
#include <WebSerial.h>
```

### Initialize the library

```cpp
AsyncWebServer server(80);
WebSerial webSerial;
```

### Use the library

```cpp
void setup() {
 webSerial.begin(&server);
 server.begin();
}

void loop() {
 webSerial.loop();
}
```

### Send data to the WebSerial

```cpp
webSerial.println("Hello, World!");
webSerial.printf("Hello, %s!", "World");
```

### Receive data from the WebSerial

You can use the `onMessage` method to receive data from the WebSerial. The method accepts a callback function that will be called when data is received. The callback function can accept both `const char *` and `String` data types.

```cpp
webSerial.onMessage([](const char *data, size_t len) {
  Serial.write(data, len);
});

webSerial.onMessage([](const String &msg) {
  Serial.println(msg);
});
```

### Connect to the device serial page

Navigate to `http://<device-ip>/webserial` to access the serial page.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

