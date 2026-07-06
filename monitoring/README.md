### Install node exporter

#### 1. Add user node_exporter
```bash
sudo useradd -rs /bin/false node_exporter
```

#### 2. Download node_exporter
```bash
export VERSION=1.11.1
wget -c https://github.com/prometheus/node_exporter/releases/download/v${VERSION}/node_exporter-${VERSION}.linux-amd64.tar.gz
```

#### 3. Extract node_exporter

```shell
tar xvf node_exporter-0.18.1.linux-amd64.tar.gz
```

#### 4. Copy node_exporter to /opt

```shell
sudo mv node_exporter-0.18.1.linux-amd64 /opt/node_exporter
sudo chown -R node_exporter:node_exporter /opt/node_exporter
```

#### 5. Create service file for systemd

```shell
sudo nano /etc/systemd/system/node_exporter.service
```

#### 6. Fillin as follows:

```config
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/opt/node_exporter --collector.systemd

[Install]
WantedBy=multi-user.target
```

#### 7. Start the service with systemd and verify it runs

```shell
sudo systemctl daemon-reload
sudo systemctl start node_exporter
sudo systemctl enable node_exporter
```

