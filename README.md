# CIDR Splitter — Visual Subnet Calculator

A modern, single-file HTML subnet calculator that lets you visually split and join CIDR blocks, with cloud provider IP reservation awareness.

![CIDR Splitter screenshot](https://raw.githubusercontent.com/snarkbe/CIDRsplitter/master/images/screenshot.png)

## Features

- **Visual split & join** — click Split to divide any subnet in two; the shared Join button spans both siblings so you can merge them back in one click
- **Cloud provider modes** — select AWS, Azure, GCP or None to see how many IPs each provider reserves per subnet and why
  - **AWS** — 5 reserved: network, VPC router (`.1`), DNS (`.2`), future use (`.3`), broadcast — [docs](https://docs.aws.amazon.com/vpc/latest/userguide/subnet-sizing.html#subnet-sizing-ipv4)
  - **Azure** — 5 reserved: network, gateway (`.1`), Azure DNS (`.2`–`.3`), broadcast — [docs](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-faq#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)
  - **GCP** — 4 reserved: network, default gateway (`.1`), second-to-last (future use), broadcast — [docs](https://docs.cloud.google.com/vpc/docs/subnets#unusable-ip-addresses-in-every-subnet)
- **Reserved IP tooltip** — hover the red badge in the Reserved IPs column to see every reserved address and its purpose
- **Cloud-adjusted usable host count** — the Usable Hosts column automatically subtracts cloud-reserved IPs
- **Copy CIDR** — click the clipboard icon next to any subnet to copy e.g. `10.0.0.0/24` to the clipboard
- **Bookmarkable state** — the full split tree is encoded in the URL; bookmark or share it and the exact layout is restored
- **Toggleable columns** — show/hide: Subnet, First Host, Last Host, Broadcast, Usable Hosts, Reserved IPs, Subnet Mask, Hex Mask, Size, Depth
- **No dependencies** — pure HTML + CSS + vanilla JavaScript, single file, works offline

## Usage

Open `index.html` directly in any modern browser — no build step, no server needed.

1. Enter a network address and prefix length, then click **Update**
2. Click **✂ Split** on any row to divide it into two equal halves
3. Click **⭠ Join** (shared between two sibling rows) to merge them back
4. Select a cloud provider to see reserved IPs and adjusted host counts
5. Hover the red badge in the **Reserved IPs** column for a breakdown
6. Click **⎘** next to any subnet to copy its CIDR notation
7. Bookmark the page URL to save your subnetting layout

## Live Demo

> [https://gh.reichert.be/CIDRsplitter/](https://gh.reichert.be/CIDRsplitter/)

## Inspiration

Inspired by [David Clayworth's Visual Subnet Calculator](https://www.davidc.net/sites/default/subnets/subnets.html), rebuilt with a modern dark UI and cloud-aware features.

## License

MIT
