# Spotify Ad Blocker for Linux and macOS

A simple, zero-resource Spotify ad blocker for Linux and macOS using `/etc/hosts` domain blocking. Run once, forget about ads.

## Features

- Blocks all Spotify ad domains – audio, video, banners, and tracking
- Zero system resource usage – no background processes, no CPU/RAM drain
- Instant ad skipping – ads fail to load immediately, no waiting
- Persists across reboots – set it and forget it
- Works with any Spotify install – .deb, Snap, Flatpak, or official binary

## How It Works

The script adds a list of ad and tracking domains to `/etc/hosts`, redirecting them to `0.0.0.0` (nowhere). When Spotify tries to fetch an ad, the request fails instantly and the ad is skipped.

## Installation

### 1. Download the script

    git clone https://github.com/artfix/spotify-ad-blocker.git
    cd spotify-ad-blocker

### 2. Make it executable

    chmod +x spotify-ad-blocker.sh

### 3. Run it once

    ./spotify-ad-blocker.sh

### 4. Restart PC

    sudo reboot now

That's it. No further steps required.

## Install for MAC users (eperimental)

Install for macOS is the same like for linux, git clone `spotify-ad-blocker-mac.sh` make it executable and run it.

⚠️ One Important macOS-Specific Note

System Integrity Protection (SIP): On modern Macs (macOS 10.15+), SIP protects /etc/hosts from being modified, but only in recovery mode. In normal operation, you can edit /etc/hosts with sudo – the script's sudo command will work fine. If you get a "Operation not permitted" error, that means SIP is blocking it, and you'd need to boot into Recovery Mode and run csrutil disable (not recommended unless you know what you're doing).

## What Gets Blocked

The script blocks the following domains:

    pubads.g.doubleclick.net
    securepubads.g.doubleclick.net
    www.googletagservices.com
    gads.pubmatic.com
    ads.pubmatic.com
    tpc.googlesyndication.com
    pagead2.googlesyndication.com
    googleads.g.doubleclick.net
    adclick.g.doublecklick.net
    adeventtracker.spotify.com
    ads-fa.spotify.com
    analytics.spotify.com
    audio2.spotify.com
    audio-ak-spotify-com.akamaized.net
    audio-ak.spotify.com.edgesuite.net
    audio-ake.spotify.com.edgesuite.net
    audio-ake.spotify.com
    b.scorecardresearch.com
    bounceexchange.com
    bs.serving-sys.com
    content.bitsontherun.com
    core.insightexpressai.com
    crashdump.spotify.com
    d2gi7ultltnc2u.cloudfront.net
    d3rt1990lpmkn.cloudfront.net
    desktop.spotify.com
    doubleclick.net
    ds.serving-sys.com
    googleadservices.com
    gtssl2-ocsp.geotrust.com
    js.moatads.com
    log.spotify.com
    media-match.com
    omaze.com
    open.spotify.com
    pagead46.l.doubleclick.net
    partner.googleadservices.com
    redirector.gvt1.com
    s0.2mdn.net
    spclient.wg.spotify.com
    v.jwpcdn.com
    video-ad-stats.googlesyndication.com
    weblb-wg.gslb.spotify.com
    www.googleadservices.com
    www.omaze.com

## Uninstalling

To revert the changes, remove the Spotify section from `/etc/hosts`:

    sudo nano /etc/hosts

Delete the lines between `# === Spotify Ad Blocking` and the last blocked domain, then save.

## Troubleshooting

### Ads still appear?

Some new ad domains may appear over time. To catch them:

    sudo journalctl -f | grep spotify

Play a song and wait for an ad. Look for connection attempts to unknown domains, then add them to `/etc/hosts` using the same format.

### Permission denied?

Make sure you run the script with `sudo`:

    sudo ./block-spotify-ads.sh

### Spotify installed via Snap/Flatpak?

Works the same. The script blocks at system level, so any Spotify installation type is affected.

## License

MIT

## Disclaimer

This tool modifies your system's hosts file to block ad domains. Use at your own discretion. Spotify's terms of service prohibit ad blocking — this is for educational purposes.
