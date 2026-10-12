# CIDR Calculator

A companion page (`calculator.html`), in the same visual style, for looking up **one** CIDR block's details rather than splitting a tree of subnets. Inspired by [cidr.xyz](https://cidr.xyz/).

[Live demo](https://gh.reichert.be/CIDRsplitter/calculator.html) · [Back to the overview](../README.md)

## Features

- **Binary breakdown**: 32 clickable bit cells, grouped into octets, show the IP in binary. Click any bit to toggle it. Bits are coloured network (accent) or host (green) according to the current prefix.
- **Prefix slider**: drag to change the prefix length live, or jump to common prefixes (`/8`, `/16`, `/20`, `/24`, `/27`, `/28`, `/30`, `/32`) with the quick-select pills.
- **Paste-aware input**: paste a bare IP or a full `x.y.z.a/b` CIDR into the IP field. A pasted CIDR splits itself into address and prefix automatically.
- **Full results grid**: CIDR notation, network and broadcast address, subnet mask, wildcard mask, hex mask, total addresses, usable hosts, first and last host, IP range.
- **Cloud provider awareness**: the same AWS, Azure and GCP reserved-IP logic as the [Splitter](splitter.md), with a live reserved-IP table and a cloud-adjusted usable host count.
- **Copy CIDR** and **Share Link**: copy the current CIDR, or a URL that restores the exact IP, prefix and provider.
- **Light and dark themes**, and the same tool tabs as the other pages. Switching tabs opens the Splitter on the current block and provider, or the [Overlap Checker](overlap-checker.md) with that block as its address space.
- **FAQ**: lookup-focused questions on wildcard masks, mask ↔ CIDR conversion, usable hosts in a /24, `/31` and `/32`, and cloud reserved IPs.
