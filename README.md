# snell install

`apt update

https://github.com/surge-networks/snell/releases/download/v2.0.3/snell-server-v2.0.3-linux-amd64.zip

touch /etc/init.d/rc.local

chmod +x /etc/init.d/rc.local

ln -s /etc/init.d/rc.local  /etc/rc.local

update-rc.d rc.local start 99 2 3 4 5 . stop 99 0 1 6 .

nano /etc/rc.local

#! /bin/sh -e

sudo -i ./snell-server

exit 0

wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh"
chmod +x tcp.sh
./tcp.sh`



## Highlights

* Extreme performance.
* Snell v2 supports reusing TCP connections to improve performance and reduce latency.
* Single binary with zero dependency. (except glibc)
* A wizard to help you start.
* Traffic obfuscating is embedded. (HTTP & TLS)
* Proxy server will report remote errors to client if encounters. Clients may choose countermeasures for different scenarios.
* The server-side program is able to auto-negotiate cipher and version with clients.
* Protocol is ready for multiple users ACL. (No implementation yet)

## Quickstart

1. Download the binary from the [Release page](https://github.com/surge-networks/snell/releases/latest).
2. Decompress and execute the binary. A wizard will guide you to generate a new config.
3. Re-execute the binary to start service.
4. Add a proxy line in Surge  (The latest beta version is required)

`Proxy = snell, [SERVER ADDRESS], [GENERATED PORT], psk=[GENERATED PSK], obfs=http`

### Use systemd for autostart (Optional)

1. Download `systemd-example` and save as `/lib/systemd/system/snell.service`
2. Reload systemd daemon: `sudo systemctl daemon-reload`
3. Move `snell-server` to `/usr/local/bin/snell-server`
4. Move `snell-server.conf` to `/etc/snell-server.conf`
5. Enable service autostart: `sudo systemctl enable snell.service`
6. Start snell service: `sudo systemctl start snell.service`
7. Verify service start successfully: `sudo systemctl status snell.service`

## Opens Source

We haven't decided whether to open source the project for complicated reasons.
