# snell

An encrypted proxy service program

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

### Systemd

1. Download `systemd-example` and save as `/lib/systemd/system/snell.service`
2. Reload systemd daemon: `sudo systemctl daemon-reload`
3. Move `snell-server` to `/usr/local/bin/snell-server`
4. Move `snell-server.conf` to `/etc/snell-server.conf`
5. Enable service autostart: `sudo systemctl enable snell.service`
6. Start snell service: `sudo systemctl start snell.service`
7. Verify service start successfully: `sudo systemctl status snell.service`

*/lib/systemd/system/snell.service*
```
[Unit]
Description=Snell Proxy Service
After=network.target

[Service]
Type=simple
User=nobody
Group=nogroup
LimitNOFILE=32768
ExecStart=/usr/local/bin/snell-server -c /etc/snell-server.conf
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=snell-server

[Install]
WantedBy=multi-user.target
```

Redirect *stdout* and *stderr* to `syslog`, if you want a separated log file, add a rsyslog config and restart `rsyslog` service

*/etc/rsyslog.d/snell-server.conf*
```
if $programname == 'snell-server' then /var/log/snell-server.log
& stop
```

## Opens Source

We haven't decided whether to open source the project for complicated reasons.
