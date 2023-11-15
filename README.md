# Rust HTTPS Client for the ESP32-C3 chip

Tested on the [Rust ESP Board](https://github.com/esp-rs/esp-rust-board).

On run, it automatically builds the firmware, flashes the connected board and monitors its console.
You may customize this behaviour in the `.cargo/config.toml` file.

**Run in Windows PowerShell:**

```shell
$env:SSID="your_wifi_ssid"; $env:PASSWORD="your_wifi_password"; cargo run --release; $env:SSID=$null; $env:PASSWORD=$null;
```

**Run in Linux:**
```shell
SSID="your_wifi_ssid" PASSWORD="your_wifi_password" cargo run --release
```

*Note*: If you try running it without the `--release` flag you will get errors related to no free memory 
for allocation in the TLS connect.

## Logic

1. Initializes the controller and enables the ESP wi-fi client.
2. Initializes Embassy tasks and executor.
3. Connects to your access point using the specified `your_wifi_ssid` and `your_wifi_password`
4. Gets an IP address from the DHCP server in your network.
5. Connects via HTTPS to the www.google.com website, checks its certificate using the stored PEM file 
in `.src/certs/www.google.com.pem`, and establishes an encrypted connection.
6. Tries to GET www.google.com/notfound page.
7. Receives result from the server and prints it to the console. 


## This project is based on:

- [embassy](https://github.com/embassy-rs/embassy)
- [ESP32 Rust no_std training](https://github.com/esp-rs/no_std-training)
- [esp-mbedtls](https://github.com/esp-rs/esp-mbedtls)

## License

Licensed under either of:

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
- MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.

## Author

Slava Dobromyslov <slava@dobromyslov.com>