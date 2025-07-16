# Useful notes for ec2 instance in AWS:

## Notes:

- increased the memory with the swap file:
  **source**: https://stackoverflow.com/questions/66693201/npm-install-hangs-forever-in-ec2

```
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap  /swapfile
sudo swapon /swapfile
sudo swapon  --show
sudo free -h
```

- to make the swapfile persistent across reboot (run as root):

```
sudo echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```
