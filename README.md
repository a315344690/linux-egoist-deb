#  EGOIST Kernel for Debian/Ubuntu

Based on the Debian generic and cloud kernel configuration file

## For Arm64 only

## Installation

You need to have `wget` and `jq` installed in advance.


```
wget -q --show-progress $(wget -q -O - https://api.github.com/repos/a315344690/linux-egoist-deb/releases/latest | jq -r '.assets[] | select(.name | contains ("deb")) | select(.name | contains ("cloud")) | .browser_download_url')
sudo dpkg -i linux-headers-*-egoist-cloud_*.deb
sudo dpkg -i linux-image-*-egoist-cloud_*.deb
```


## Patches

- Graysky's Kernel patch enables compiler optimizations for additional CPUs
- Broadcom fullcone NAT from ASUS Merlin (IPv4 only)
- Netfilter FLOWOFFLOAD target
- BBRv3
- Cloudflare: Add a sysctl to skip tcp collapse processing when the receive buffer is full ([How-to-use](https://blog.cloudflare.com/optimizing-tcp-for-high-throughput-and-low-latency/))
- TCP Brutal
- Partial Clear Linux patches

## Notice

1. **This kernel has a built-in TCP Brutal module, please do not use the official installation script to install the DKMS module.**
2. I **hardcoded** the enable parameter for fullcone to prevent recompiling iptables or adding nftables parameters to use fullcone, so you can use MASQUERADE as usual, and it will **force** to using fullcone.

