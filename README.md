# wpa_supplicant for broadcom-wl >=6.30.223.x
`wpa_supplicant` version 2.7 and 2.8 are incompatible with the `broadcom-wl` Linux driver (see [this](https://bugzilla.redhat.com/show_bug.cgi?id=1703745), [this](https://www.reddit.com/r/Fedora/comments/ce3bsf/wifi_not_working_after_update_to_fedora_30/?utm_source=share&utm_medium=web2x), and [this](https://www.reddit.com/r/Fedora/comments/bj95zy/wifi_stuck_on_connecting_after_upgrade_to_fedora/?utm_source=share&utm_medium=web2x)). This repo contains a patched version of `wpa_supplicant` **2.8** to make it compatible again.
The code in this repo is tested and works on a laptop with the BCM4360 chip, running Fedora 30.

Although I intend to keep this repo up-to-date, I cannot guarantee that the latest release is build against the lastest version of `wpa_supplicant`. If the code in this repo it outdated, feel free to open an issue.

## Source
The patches in this repo were developed by [dcaratti](https://copr.fedorainfracloud.org/coprs/dcaratti/wpa_supplicant/). There is no difference between the code in his COPR repo and the code in my GitHub repo. If you're using Fedora, you may want to use his COPR repo instead of compiling `wpa_supplicant` yourself.

## Installation guide
If you're running Fedora, the easiest way to install would be by using [dcarrati's COPR repository](https://copr.fedorainfracloud.org/coprs/dcaratti/wpa_supplicant/). 
Alternatively, download the [latest release](https://github.com/REijkelenberg/wpa_supplicant-broadcom-wl/releases) from this GitHub repo and run `dnf install /path/to/wpa_supplicant_binary.rpm`.

Make sure to blacklist `wpa_supplicant` in your package manager to prevent it from being replaced by a future, unpatched version.
If you're using `dnf`, add the line `exclude=wpa_supplicant` to /etc/dnf/dnf.conf.

### Compilation guide (Fedora or other distros using RPM)
1. Install `rpm-build` (e.g. `dnf install rpm-build`)
2. Place the contents of this repo in ~/rpmbuild/SOURCES
3. `cd` to ~/rpmbuild/SOURCES/
4. Run `rpmbuild -bb wpa_supplicant.spec`
5. The compiled binary will be placed in ~/rpmbuild/RPMS

Note: `rpmbuild` may complain about missing dependencies. Install these with e.g. `dnf install <dependencies>`.

## License
`wpa_supplicant` is licensed under a [BSD license](http://w1.fi/cgit/hostap/plain/wpa_supplicant/README).
