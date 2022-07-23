sudo mkdir /usr/local/share/ca-certificates/extra
sudo cp  app.crt /usr/local/share/ca-certificates/extra/.
sudo update-ca-certificates
ls -l /etc/ssl/certs/app*
nsenter --target 1 --mount systemctl restart containerd