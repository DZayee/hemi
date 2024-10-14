# hemi
Update Hemi

sudo systemctl stop popmd
rm -rf heminetwork_v0.4.4_linux_amd64 && rm -rf heminetwork 

wget https://github.com/hemilabs/heminetwork/releases/download/v0.4.5/heminetwork_v0.4.5_linux_amd64.tar.gz && tar xvf heminetwork_v0.4.5_linux_amd64.tar.gz
Config lại Systemd
vi /etc/systemd/system/popmd.service
From: WorkingDirectory=/root/heminetwork_v0.4.4_linux_amd64
      ExecStart=/root/heminetwork_v0.4.4_linux_amd64/popmd
To:   WorkingDirectory=/root/heminetwork_v0.4.5_linux_amd64
      ExecStart=/root/heminetwork_v0.4.5_linux_amd64/popmd

[Unit]
Description=PoPM Service
After=network.target

[Service]
EnvironmentFile=/etc/popmd_env
WorkingDirectory=/root/heminetwork_v0.4.5_linux_amd64
ExecStart=/root/heminetwork_v0.4.5_linux_amd64/popmd
Restart=always
RestartSec=5

[Install]
WantedBy=multi

Reload lại systemd
sudo systemctl daemon-reload
sudo systemctl restart popmd
