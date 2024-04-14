# Linux on Lenovo Yoga 9 2-in-1 14IMH9

I recently purchased a 2024 Lenovo Yoga 9i and installed Arch Linux (linux-zen 6.8.0). Here is how I got everything working.

## OOTB Experience

Everything works, except:

- Fingerprint
- Bass speakers

## Fingerprint

Fixing the fingerprint sensor is easy. You simply need to add the PID `27c6:650c` to libfprint. I have submitted the [patch](fingerprint/0001-goodixmoc-Add-PID-0x650C.patch) to upstream and it has been [merged](https://gitlab.freedesktop.org/libfprint/libfprint/-/merge_requests/470).

For now, you need to build libfprint from the latest source. Once a new version of libfprint is released, it should work out of the box.

## Bass speakers

The bass speakers are a bit more tricky. Unlike previous models, 14IMH9 uses CS35L41 amplifiers, and the [existing patch](https://github.com/PJungkamp/yoga9-linux/) is not able to activate them.

To enable the bass speakers and volume control, apply the [kernel patch](speakers/0001-ALSA-hda-realtek-Add-quirk-for-Lenovo-Yoga-9-14IMH9.patch). The patch has been [merged](https://git.kernel.org/pub/scm/linux/kernel/git/tiwai/sound.git/commit/?id=9b714a59b719b1ba9382c092f0f7aa4bbe94eba1) by the upstream, and will probably land in kernel 6.9 (**Update**: This has been backported to 6.8.6).

While the kernel patch alone is able to enable the bass speakers, it uses generic firmware by default, and sound quality can be significantly improved by extracting the firmware from the Windows driver. Follow [this guide](https://gist.github.com/masselstine/8fe9634b4c31cef07b8dfab089e4eb38#sound) if you are interested. Take note that the guide is for a different laptop, ignore everything other than the firmware extraction steps.
