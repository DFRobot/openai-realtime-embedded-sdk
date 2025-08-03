# Open RealtimeAPI Embedded SDK

# Table of Contents

- [Docs](#docs)
- [Installation](#installation)
- [Usage](#usage)

## Platform/Device Support

This SDK has been developed tested on a `esp32s3` and `linux`. You don't need any physical hardware
to run this SDK. You can use it from Linux directly.

To use it on hardware purchase either of these microcontrollers. Others may work, but this is what
has been developed against.

* [Freenove ESP32-S3-WROOM](https://www.amazon.com/gp/product/B0BMQ8F7FN)
* [Sonatino - ESP32-S3 Audio Development Board](https://www.amazon.com/gp/product/B0BVY8RJNP)

You can get a ESP32S3 for much less money on eBay/AliExpress.

## Installation

Call `set-target` with the platform you are targetting. Today only `linux` and `esp32s3` are supported.
* `idf.py set-target esp32s3`

Configure device specific settings. None needed at this time
* `idf.py menuconfig`

Set your Wifi SSID + Password as env variables
* `export WIFI_SSID=foo`
* `export WIFI_PASSWORD=bar`
* `export OPENAI_API_KEY=bing`

Build
* `idf.py build`

If you built for `esp32s3` run the following to flash to the device
* `sudo -E idf.py flash`

If you built for `linux` you can run the binary directly
* `./build/src.elf`

See [build.yaml](.github/workflows/build.yaml) for a Docker command to do this all in one step.

### Full Installation Guide
#### Export Wifi Credentials and OpenAI API Key
You need to export your Wifi credentials and OpenAI API Key as environment variables. This is required for the SDK to connect to the internet and access OpenAI services.

```bash
export WIFI_SSID="your_wifi_ssid"
export WIFI_PASSWORD="your_wifi_password"
export OPENAI_API_KEY="your_openai_api_key"
```

#### Install correct version of ESP-IDF
```bash
mkdir ~/esp
cd ~/esp
git clone -b release/v5.5 https://github.com/espressif/esp-idf.git esp-idf-v5.5.0
cd esp-idf-v5.5.0
./install.sh
chmod 777 ./export.sh
./export.sh 
```

#### Test IDF
`idf.py --version`
The above didn't work for me so I included this line in ~/.bashrc and reloaded the terminal: `. $HOME/esp/esp-idf-v5.5.0/export.sh`

#### Clone repo including dependencies
```bash
git clone --recursive https://github.com/DFRobot/openai-realtime-embedded-sdk.git
cd openai-realtime-embedded-sdk
```

#### Set target
`idf.py set-target esp32s3`

#### Build
`idf.py build`

#### Allow idf.py flash to be used with current user
`sudo usermod -a -G dialout $USER`

#### Flash to device
`idf.py flash`