# Simple NTP server container via chronyd

- Uses local stratum by default (host clock)
- Contains an example with md5 encryption (legacy)

## Use a remote ntp server pool

In `chrony.conf` replace

```
local stratum 8
```

with

```
pool pool.ntp.org iburst
initstepslew 10 pool.ntp.org
```

## Build on foreign architecture (eg. ARM)

```bash
sudo dnf install qemu-user-static
sudo podman run --rm --privileged multiarch/qemu-user-static --reset -p yes
podman build --arch=arm -t ntp-server-local -f Dockerfile .
```

### Build with encryption support

```bash
podman build --arch=arm -t ntp-server-local -f Dockerfile .
podman build --arch=arm -t ntp-server-local:enc -f Dockerfile.enc .
```
