# Subnet Splitter

The main page (`index.html`): split and join IPv4 CIDR blocks visually, with cloud provider IP reservation awareness.

[Live demo](https://gh.reichert.be/CIDRsplitter/) · [Back to the overview](../README.md)

![CIDR Splitter screenshot](../images/screenshot.png)

## Quick start

1. Enter a network address and prefix length, then click **Update**
2. Click **✂ Split** on a row to halve it, or **⊟ /x** to divide it into equal subnets of a target prefix in one step
3. Click **⭠ Join** (shared between two sibling rows) to merge them back
4. Type an optional **Name** next to any subnet; it's used in exports and auto-generated if left blank
5. Pick a cloud provider to see reserved IPs, adjusted host counts and provider export fields
6. Untick a subnet's checkbox to leave it out of exports
7. Use the **Export** buttons, or bookmark the URL to save the whole layout

## Splitting and naming

- **Visual split & join**: Split divides any subnet in two. The shared Join button spans both siblings, so you can merge them back in one click.
- **Split to a prefix**: divide a block into equal subnets of a chosen prefix (a `/16` straight into `/24`s) instead of halving repeatedly.
- **Per-subnet names**: names follow the first half when you split and carry over when you join. Empty names fall back to an auto-generated label such as `subnet-1-10-0-0-0-24` in exports.
- **Toggleable columns**: Subnet, Name, First Host, Last Host, Broadcast, Usable Hosts, Reserved IPs, Subnet Mask, Hex Mask, Size, Depth.
- **Copy CIDR**: the clipboard icon next to a subnet copies e.g. `10.0.0.0/24`.

## Cloud providers

Select AWS, Azure, GCP or None. The Usable Hosts column subtracts the addresses the provider reserves, and hovering the red badge in the Reserved IPs column lists each one and why.

| Provider | Reserved | Addresses | Source |
|---|---|---|---|
| AWS | 5 | network, VPC router (`.1`), DNS (`.2`), future use (`.3`), broadcast | [docs](https://docs.aws.amazon.com/vpc/latest/userguide/subnet-sizing.html#subnet-sizing-ipv4) |
| Azure | 5 | network, gateway (`.1`), Azure DNS (`.2`–`.3`), broadcast | [docs](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-faq#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets) |
| GCP | 4 | network, default gateway (`.1`), second-to-last (future use), broadcast | [docs](https://docs.cloud.google.com/vpc/docs/subnets#unusable-ip-addresses-in-every-subnet) |

### Azure helpers

- **Subnet sizing guide**: a collapsible reference, shown and opened when Azure is selected. It gives minimum and recommended sizes for GatewaySubnet, AzureFirewallSubnet, AzureFirewallManagementSubnet, AzureBastionSubnet, RouteServerSubnet, Application Gateway v2, API Management v2 and Container Instances, each linked to its Microsoft Learn source.
- **Reserved-name checks**: with Azure selected, typing a platform-reserved name (e.g. `AzureBastionSubnet`) in the Name column flags a subnet that's too small, suggests the right spelling for near-miss typos (`AzureBasdtionSubnet` → *Did you mean AzureBastionSubnet?*) and flags duplicate names. The same warnings are written as comments into the Azure CLI, Terraform and Bicep exports.

## Exports

| Format | Content |
|---|---|
| **CSV** / **TXT** | the table as data, or as an aligned text grid |
| **Markdown** | a GitHub-flavored table (numeric columns right-aligned), ready for a README, wiki or PR |
| **JSON** | structured `{ provider, subnets[] }` with CIDR, hosts, broadcast, etc. |
| **CLI** | a ready-to-run script: `az network vnet subnet create`, `aws ec2 create-subnet` or `gcloud compute networks subnets create` |
| **Terraform** | `azurerm_subnet`, `aws_subnet` or `google_compute_subnetwork` resources |
| **Native IaC** | Bicep (Azure) or CloudFormation (AWS) |

- **Selective export**: tick or untick each subnet (or the header "select all") to control exactly what appears in every export.
- **Provider-specific fields**: once a cloud is selected, the optional details baked into exports are VPC ID (AWS), Resource Group and VNet (Azure), or Project, Network and Region (GCP).

## State, themes and navigation

- **Bookmarkable state**: the split tree, subnet names, provider, provider fields and per-row export selection are encoded in the URL. Bookmark or share it and the exact setup comes back.
- **Light and dark themes**: toggle in the top-right corner. Your choice is remembered and defaults to your OS preference.
- **Tool tabs**: switch to the [CIDR Calculator](calculator.md) or the [Overlap Checker](overlap-checker.md). The current root block and provider carry over.
- **FAQ**: an on-page FAQ covers how many IPs AWS, Azure and GCP reserve, and why usable host counts differ.
