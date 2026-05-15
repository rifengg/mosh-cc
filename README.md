# Mosh for Claude Code

A fork of [Mosh](https://mosh.org/) with patches for
[Claude Code](https://docs.anthropic.com/en/docs/claude-code) on remote VPS
environments.

We run Claude Code on Hetzner VPS instances and connect via Mosh. A few terminal
rendering features that Claude Code uses (dim text, strikethrough) aren't in the
current Mosh release. This fork cherry-picks the upstream PRs that add them.

If you have a similar setup, this might save you some time.

> Not affiliated with or endorsed by Anthropic or the Mosh project.

## What's included

See [PATCHES.md](PATCHES.md) for the full list. In short:

- **SGR 2 (dim/faint text) + SGR 9 (strikethrough)** — Claude Code's agent view uses
  dim text for dashboard dividers. Stock Mosh strips these. From upstream
  [PR #1380](https://github.com/mobile-shell/mosh/pull/1380).
- **config.h build fix** — Corrects inconsistent codepath compilation. From upstream
  [PR #1382](https://github.com/mobile-shell/mosh/pull/1382).

All patches come from existing upstream PRs. We haven't written any new Mosh features.

## Install

### macOS (client)

```
brew tap rifengg/mosh-cc
brew install mosh-cc
```

### Ubuntu/Debian (server, e.g. Hetzner VPS)

Download the `.deb` from the
[latest release](https://github.com/rifengg/mosh-cc/releases/latest).
The .deb is built on Ubuntu 22.04. For other versions, build from source.

```
curl -LO https://github.com/rifengg/mosh-cc/releases/download/v1.5.0-cc.1/mosh-cc_1.5.0-cc.1_amd64.deb
sudo dpkg -i mosh-cc_1.5.0-cc.1_amd64.deb
```

### Build from source

```
sudo apt install protobuf-compiler libprotobuf-dev libutempter-dev \
  libncurses5-dev zlib1g-dev libssl-dev automake autoconf libtool pkg-config

git clone https://github.com/rifengg/mosh-cc.git
cd mosh-cc
./autogen.sh && ./configure --program-suffix=-cc && make
sudo make install
```

macOS build dependencies: `brew install protobuf pkg-config automake autoconf libtool`

## Usage

Works exactly like Mosh. Install `mosh-cc` on both client and server for best results.
If only one side has the patches, you'll get stock Mosh behavior for the missing features
(dim text won't render as dim, etc.) — nothing breaks, you just don't get the fix.

```
mosh-cc user@your-vps.example.com
```

To use the patched server explicitly (e.g. if stock Mosh is also installed):

```
mosh --server=/usr/local/bin/mosh-server-cc user@your-vps.example.com
```

## License

GPLv3, same as Mosh. See [COPYING](COPYING).
