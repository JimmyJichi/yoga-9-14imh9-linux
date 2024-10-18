# Linux on Lenovo Yoga 9 2-in-1 14IMH9

I recently purchased a 2024 Lenovo Yoga 9i and installed Arch Linux (linux-zen 6.8.0). Here is how I got everything working.

**Update: As of October 2024, everything should work out of the box with the latest kernel and libfprint. You may ignore the following information except (optionally) the part about audio firmware.**

## OOTB Experience

Everything works, except:

- Fingerprint
- Bass speakers

## Fingerprint

Fixing the fingerprint sensor is easy. You simply need to add the PID `27c6:650c` to libfprint. I have submitted the [patch](fingerprint/0001-goodixmoc-Add-PID-0x650C.patch) to upstream and it has been [merged](https://gitlab.freedesktop.org/libfprint/libfprint/-/merge_requests/470).

For now, you need to build libfprint from the latest source, or install [libfprint-git](https://aur.archlinux.org/packages/libfprint-git) if you're on Arch. Once a new version of libfprint is released, it should work out of the box.

## Bass speakers

The kernel patch that enables the bass speakers has been backported to 6.8.6.

While the kernel patch alone is able to enable the bass speakers, it uses generic firmware by default, and sound quality can be significantly improved by extracting the firmware from the Windows driver. Follow [this guide](https://gist.github.com/masselstine/8fe9634b4c31cef07b8dfab089e4eb38#sound) if you are interested. Take note that the guide is for a different laptop, ignore everything other than the firmware extraction steps.
