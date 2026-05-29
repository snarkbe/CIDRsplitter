# CIDR Splitter — Visual Subnet Calculator

A modern, single-file HTML subnet calculator that lets you visually split and join CIDR blocks, with cloud provider IP reservation awareness.

![CIDR Splitter screenshot](https://raw.githubusercontent.com/snarkbe/CIDRsplitter/master/images/screenshot.png)

## Features

- **Visual split & join** — click Split to divide any subnet in two; the shared Join button spans both siblings so you can merge them back in one click
- **Split to a prefix** — divide a block into equal subnets of a chosen prefix (e.g. a `/16` straight into `/24`s) in one step, instead of halving repeatedly
- **Per-subnet names** — give any subnet an optional name; names follow the first half when you split and carry over when you join. Empty names fall back to an auto-generated label (e.g. `subnet-1-10-0-0-0-24`) in exports
- **Cloud provider modes** — select AWS, Azure, GCP or None to see how many IPs each provider reserves per subnet and why
  - **AWS** — 5 reserved: network, VPC router (`.1`), DNS (`.2`), future use (`.3`), broadcast — [docs](https://docs.aws.amazon.com/vpc/latest/userguide/subnet-sizing.html#subnet-sizing-ipv4)
  - **Azure** — 5 reserved: network, gateway (`.1`), Azure DNS (`.2`–`.3`), broadcast — [docs](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-faq#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)
  - **GCP** — 4 reserved: network, default gateway (`.1`), second-to-last (future use), broadcast — [docs](https://docs.cloud.google.com/vpc/docs/subnets#unusable-ip-addresses-in-every-subnet)
- **Reserved IP tooltip** — hover the red badge in the Reserved IPs column to see every reserved address and its purpose
- **Cloud-adjusted usable host count** — the Usable Hosts column automatically subtracts cloud-reserved IPs
- **Provider-specific export fields** — when a cloud is selected, fill in the optional details that get baked into exports: VPC ID (AWS), Resource Group & VNet (Azure), or Project, Network & Region (GCP)
- **Export suite** — download your layout in any format:
  - **CSV** / **TXT** — the table as data or an aligned text grid
  - **JSON** — structured `{ provider, subnets[] }` with CIDR, hosts, broadcast, etc.
  - **CLI** — a ready-to-run shell script for the selected provider (`az network vnet subnet create`, `aws ec2 create-subnet`, or `gcloud compute networks subnets create`)
  - **Terraform** — `azurerm_subnet`, `aws_subnet`, or `google_compute_subnetwork` resources
  - **Native IaC** — Bicep (Azure) or CloudFormation (AWS)
- **Selective export** — tick/untick the checkbox next to each subnet (or the header "select all") to control exactly which subnets appear in every export
- **Copy CIDR** — click the clipboard icon next to any subnet to copy e.g. `10.0.0.0/24` to the clipboard
- **Bookmarkable state** — the full split tree, subnet names, selected provider, provider fields, and per-row export selection are encoded in the URL; bookmark or share it and the exact setup is restored
- **Light & dark themes** — toggle with the button in the top-right corner; your choice is remembered and defaults to your OS preference
- **Toggleable columns** — show/hide: Subnet, Name, First Host, Last Host, Broadcast, Usable Hosts, Reserved IPs, Subnet Mask, Hex Mask, Size, Depth
- **No dependencies** — pure HTML + CSS + vanilla JavaScript, single file, works offline

## Usage

Open `index.html` directly in any modern browser — no build step, no server needed.

1. Enter a network address and prefix length, then click **Update**
2. Click **✂ Split** on any row to divide it into two equal halves, or **⊟ /x** to divide it into equal subnets of a target prefix in one step
3. Click **⭠ Join** (shared between two sibling rows) to merge them back
4. Type an optional **Name** next to any subnet (used in exports; auto-named if left blank)
5. Select a cloud provider to see reserved IPs, adjusted host counts, and provider export fields
6. Hover the red badge in the **Reserved IPs** column for a breakdown
7. Untick the checkbox next to any subnet to exclude it from exports
8. Use the **Export** buttons to download CSV, TXT, JSON, a CLI script, Terraform, or native IaC
9. Click **⎘** next to any subnet to copy its CIDR notation
10. Toggle light/dark mode with the button in the top-right corner
11. Bookmark the page URL to save your full layout (splits, names, provider, fields, and selection)

## Live Demo

> [https://gh.reichert.be/CIDRsplitter/](https://gh.reichert.be/CIDRsplitter/)

## Inspiration

Inspired by [David Clayworth's Visual Subnet Calculator](https://www.davidc.net/sites/default/subnets/subnets.html), rebuilt with a modern dark UI and cloud-aware features.

## License

MIT
