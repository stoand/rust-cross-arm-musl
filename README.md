# Cross compile Rust to `arm-unknown-linux-musleabihf`

__with dynamic C library support__

* Install the following system dependencies

```
rustup target add arm-unknown-linux-musleabihf
sudo apt-get install gcc-arm-linux-gnueabihf
```

* Clone this repo into `~/.cargo`
* Add to `.bashrc`

```
export CC_arm_unknown_linux_musleabihf=arm-linux-gnueabihf-gcc
```

* Add to `~/.cargo/config`

```
[target.arm-unknown-linux-musleabihf]
linker = "~/.cargo/rust-cross-arm-musl/arm-linux-gnueabihf-link.sh"
```
* cd `~/.cargo/rust-cross-arm-musl`
* Download and extract your needed libraries from Alpine Linux packages (listed at [http://nl.alpinelinux.org/alpine/latest-stable/main/armhf/](http://nl.alpinelinux.org/alpine/latest-stable/main/armhf/))

```
# THESE WILL VARY
# SAMPLE LIBRARIES BELOW:

wget http://nl.alpinelinux.org/alpine/latest-stable/main/armhf/libpq-9.6.3-r0.apk
wget http://nl.alpinelinux.org/alpine/latest-stable/main/armhf/libssl1.0-1.0.2k-r0.apk
wget http://nl.alpinelinux.org/alpine/latest-stable/main/armhf/libcrypto1.0-1.0.2k-r0.apk

tar --strip-components=2  -C lib/ -xzf libpq-9.6.3-r0.apk usr/lib
tar --strip-components=1  -C lib/ -xzf libssl1.0-1.0.2k-r0.apk lib
tar --strip-components=1  -C lib/ -xzf libcrypto1.0-1.0.2k-r0.apk lib
```

* Build!

```
cargo build --target arm-unknown-linux-musleabihf
```