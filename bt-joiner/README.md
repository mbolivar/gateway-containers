# Bluetooth LE 6LoWPAN joiner

## Build the container

```
docker build -t bt-joiner --force-rm -f Dockerfile<.arm64/.armhf> .
```

## Run the container

```
docker run --restart=always -d -t --privileged --net=host --read-only --tmpfs=/var/run --tmpfs=/var/lock --tmpfs=/var/log --name bt-joiner bt-joiner
```

To overwrite the default bt-joiner config values, create a local config file containing the desired options:

```
$ cat bluetooth_6lowpand.conf
HCI_INTERFACE=hci0
SCAN_WIN=3
SCAN_INT=6
MAX_DEVICES=15
```

Then start the container by overwriting bluetooth_6lowpand.conf:

```
docker run --restart=always -d -t --privileged --net=host --read-only --tmpfs=/var/run --tmpfs=/var/lock --tmpfs=/var/log -v /home/linaro/bluetooth_6lowpand.conf:/etc/bluetooth/bluetooth_6lowpand.conf --name bt-joiner bt-joiner
```

## Run the pre-built container

AMD64:

```
docker run --restart=always -d -t --privileged --net=host --read-only --tmpfs=/var/run --tmpfs=/var/lock --tmpfs=/var/log --name bt-joiner linarotechnologies/bt-joiner
```

ARM64:

```
docker run --restart=always -d -t --privileged --net=host --read-only --tmpfs=/var/run --tmpfs=/var/lock --tmpfs=/var/log --name bt-joiner linarotechnologies/bt-joiner:latest-arm64
```

ARMHF:

```
docker run --restart=always -d -t --privileged --net=host --read-only --tmpfs=/var/run --tmpfs=/var/lock --tmpfs=/var/log --name bt-joiner linarotechnologies/bt-joiner:latest-armhf
```
