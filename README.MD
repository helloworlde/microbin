# MicroBin

![Screenshot](git/index.png)

MicroBin is a super tiny and simple self hosted pastebin app written in Rust. The executable is around 6MB and it uses 2MB memory (plus your pastas).

### Installation
Simply clone the repository, build it with `cargo build --release` and run the `microbin` executable in the created `target/release/` directory. It will start on port 8080. 

To install it as a service on your Linux machine, create a file called `/etc/systemd/system/microbin.service`, paste this into it with the value of `ExecStart` replaced with the actual path to microbin on your machine.

```
[Unit]
Description=MicroBin
After=network.target
[Service]
Type=simple
Restart=always
ExecStart=/home/pi/microbin/target/release/microbin
[Install]
WantedBy=multi-user.target
```

Then start the service with `systemctl start microbin` and enable it on boot with `systemctl enable microbin`.

### Create Pasta with cURL

Simple text Pasta: `curl -d "expiration=10min&content=This is a test pasta" -X POST https://microbin.myserver.com/create`

Simple text Pasta: `curl -d "expiration=10min&content=$( < mypastafile.txt )" -X POST https://microbin.myserver.com/create`

Available expiration options:
- 1min
- 10min
- 1hour
- 24hour
- 1week
- never

Use cURL to read the pasta: `curl https://microbin.myserver.com/rawpasta/fish-pony-crow`

or to download the pasta: `curl https://microbin.myserver.com/rawpasta/fish-pony-crow > output.txt`

### Features
- Very little CSS and no JS, super lightweight and simple (see [water.css](https://github.com/kognise/water.css))
- Animal names instead of random numbers for pasta identifiers
- Automatically expiring pastas
- Never expiring pastas
- Listing and manually removing pastas
- URL shortening and redirection

### Needed improvements
- Persisting pastas on disk (currently they are lost on restart)
- Removing pasta after N reads
- File uploads
- ~~URL shortening~~ (added on 23 April 2022)
- CLI tool
- Configuration with command line arguments (ports, enable-disable pasta list, footer, etc)
