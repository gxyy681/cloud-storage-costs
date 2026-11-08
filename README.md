# Cloud Storage Server: What 1 TB Really Costs — Object Storage, Self-Hosted Software, or a Rented Server? (Plans, Prices, Per-TB Math)

Anyone shopping for a cloud storage server faces three very different prices for the same terabyte: $1.23 a month in Google's Archive tier, $20.48 a month in its Standard tier, and $79 a month as 1 TB of NVMe inside a dedicated machine that also brings 32 GB of RAM and 30 TB of bandwidth. Self-hosted software sits off to the side, free to license and expensive to run.

Which one is right depends on how often you read the data, how much of it leaves the provider's network, and whether you want a bill that changes every month. Below is the per-terabyte arithmetic for each route, the fees that make cheap storage stop being cheap, and SpinServers' current storage-capable configurations with prices attached.

> **Quick pick:** if you want root access, your own disks and a fixed monthly bill, the entry dedicated box at $79/month is the sensible starting point: Intel Xeon E3-1280 v5, 32 GB RAM, 1 TB NVMe, dual 10 Gbps ports, 30 TB of bandwidth, billed month to month in Dallas or San Jose. If you're parking under a terabyte of cold backups, no rented server will beat archive-tier object storage on price. 👉 [Check the current SpinServers dedicated server configurations and prices](https://bit.ly/Spinservers)

## What a cloud storage server actually is, in three forms

The phrase covers three purchases that look similar on an invoice line and behave nothing alike. One is capacity you rent by the gigabyte from a provider that also guarantees the data survives. One is software you install on hardware you already have. One is a physical machine in a datacenter that you operate yourself.

**Managed object storage.** You rent space, the provider keeps it alive. Data gets replicated across servers, datacenters, availability zones or regions so that a failed disk or a flooded building doesn't take your files with it. Housing, cooling, physical security, hardware monitoring and capacity planning are the provider's problem. Public cloud storage is built for multiple tenants per server, with access controls, security policies and isolation keeping customers apart; some providers sell dedicated servers where stronger isolation matters.

**Self-hosted software.** You get single-tenant control and you inherit the durability problem. Private cloud storage can live on-premises or on hardware you rent from a provider, and who runs it decides the cost structure: your own kit means hardware purchase, maintenance and operational work; a provider-run private cloud usually bills per resource plus a support tier.

**A rented server.** A VPS or bare-metal box where you install whatever storage stack you like: a file sync platform, an S3-compatible layer, or a plain filesystem with rsync and a backup script. Nobody replicates your data for you unless you configure it.

Durability is the line that separates them. On managed storage, the provider is contractually on the hook for it. On the other two, an unnoticed failed disk is your outage.

## The per-terabyte math behind "cheap" object storage

Google publishes starting rates by storage class, and converting them to terabytes (1 TB = 1,024 GiB) gives a cleaner picture than the per-gigabyte numbers.

| Storage class | Google's suggested use | Starting rate | Per TB per month |
| --- | --- | --- | --- |
| Standard | Frequently accessed data | $0.02/GiB/month | $20.48 |
| Nearline | Data stored 30 days | $0.01/GiB/month | $10.24 |
| Coldline | Data stored 90 days | $0.004/GiB/month | $4.10 |
| Archive | Data stored 365 days | $0.0012/GiB/month | $1.23 |

Those are official starting prices, and storage is only one of four billing components. The others are what turn a $1.23 terabyte into something else:

- Retrieval from Nearline, Coldline and Archive starts at $0.01/GiB, or **$10.24 per terabyte each time you read it back**.
- General egress out of Google Cloud starts at $0.08/GiB, or **$81.92 per terabyte**; transfers between continents and out of the network sit in this bucket.
- Inter-region replication for dual-region and multi-region buckets starts at $0.02/GiB ($20.48/TB).
- Operations start at $0.0004 per 1,000 requests, and Autoclass management costs $0.0025 per 1,000 objects per 30 days.

The free tier softens the entry: 5 GiB of Standard storage, 5,000 Class A and 50,000 Class B operations a month, no retrieval fee on Standard, unlimited inbound transfer, and 100 GiB a month of egress from North America to each destination (Australia and China excluded).

Run a real workload through it. Store 1 TB in Standard and you pay $20.48 a month. Download the whole library once and, after the 100 GiB free allowance, you pay about $73.92 in egress. That one transfer costs nearly as much as a month of the $79 dedicated server, which includes 30 TB of bandwidth and keeps the files on local NVMe the whole time. Archive storage is the cheapest place on earth to leave data untouched for a year, and a poor place to keep anything you open weekly.

## SpinServers' current storage-capable configurations

SpinServers sells bare metal and KVM virtual servers out of Dallas and San Jose, billed month to month with root access. The dedicated inventory is where storage capacity lives: the entry configuration carries a full terabyte of NVMe, and the two larger boxes carry multi-terabyte SSD arrays.

| Configuration | CPU / RAM | Local storage | Bandwidth | Price | Order |
| --- | --- | --- | --- | --- | --- |
| Intel Xeon E3-1280 v5 (Dallas) | 4 cores / 32 GB | 1 TB NVMe | 30 TB | $79/mo | [Deploy this server](https://bit.ly/Spinservers) |
| Intel Xeon E3-1280 v5 (San Jose) | 4 cores / 32 GB | 1 TB NVMe | 30 TB | $79/mo | [Deploy this server](https://bit.ly/Spinservers) |
| Dual Intel Xeon Gold 6148 (Dallas) | 40 vCPU / 256 GB | 3.84 TB SSD | 30 TB | $235/mo | [Deploy this server](https://bit.ly/Spinservers) |
| Dual Intel Xeon Platinum 8173M (Dallas) | 56 vCPU / 512 GB | 7.68 TB SSD | 30 TB | $390/mo | [Deploy this server](https://bit.ly/Spinservers) |

The KVM line is the cheaper way in if 100–500 GB is enough and you don't need dedicated cores:

| Plan | vCPU / RAM | Local disk | Bandwidth | Price |
| --- | --- | --- | --- | --- |
| KVM 6 vCPU 8 GB | 6 / 8 GB DDR4 | 120 GB RAID-10 SSD | 8 TB | from $39/mo |
| KVM 12 vCPU 12 GB | 12 / 12 GB DDR4 | 160 GB SSD | 10 TB | from $62/mo |

The same page also lists a 4 vCPU / 4 GB / 80 GB entry plan, an 8 vCPU / 8 GB / 160 GB plan and a 32 vCPU / 32 GB / 500 GB advanced plan; pricing for those appears at the order step and moves with availability.

Now compare the $79 box against the bucket on the axis that matters. Local NVMe at $79 for 1 TB is roughly $79 per terabyte per month, close to four times Google's Standard rate. You are not buying storage at that point, you are buying 32 GB of RAM, four cores, dual 10 Gbps ports, 30 TB of transfer and a bill that never surprises you. Pull a terabyte out of Google's network twice in a month and the egress alone ($147.84 after the free allowance) has already beaten the server's price. 👉 [Compare the full dedicated server lineup and current pricing](https://bit.ly/Spinservers)

Two things to weigh before ordering. The servers are self-managed, so the OS, the storage stack and the backups are yours to configure; and month-to-month billing keeps you flexible, but no money-back guarantee is published, so treat the first invoice as a commitment rather than a trial.

## If you'd rather run the software yourself

Three self-hosted options come up repeatedly, and they solve different problems.

**Nextcloud** is free, open-source file sync and collaboration software maintained by Germany's Nextcloud GmbH and a large contributor community. You point it at your own server or a trusted hosting provider, and you get desktop and mobile access to documents, photos, contacts and calendars, plus optional chat and video calls. Nextcloud Office runs in a browser, supports real-time co-editing, and handles DOC, DOCX, PPT, PPTX, XLS, XLSX, ODF and a long tail of other formats. A NAS is a device on your network for storing files; Nextcloud is software, and you can install it on a NAS to get both.

The hardware question has a concrete answer from Nextcloud's own guidance: an absolute minimum of 128 MB RAM, at least 512 MB recommended for the most basic single-user setup, and 3–8 GB for a full multi-user Hub installation. That last figure is why the $79 dedicated box with 32 GB is more machine than a family file share needs, and why a 4 GB VPS is not enough for a department.

**FileCloud** targets businesses that need a self-hosted file server behind their own firewall or on AWS, Windows or Linux. It bills per organization account with external users free, and the feature list is the enterprise kind: AES-256 encryption, SSL/TLS in transit, endpoint backup, two-factor authentication, SSO, Active Directory and LDAP integration, granular share permissions with expiry dates, unlimited file versioning, retention policies, PII/PHI/PCI discovery and a compliance center aimed at HIPAA, ITAR, GDPR, FINRA and CMMC. Its "unlimited storage" claim needs a caveat: the page also explains that admins expand capacity by connecting Amazon S3 or Microsoft Azure, so the unlimited part is an integration path rather than free disk. Pricing tiers aren't published as numbers.

**Zenko CloudServer** is the answer for developers who want an S3 API without renting S3. It's an Apache 2.0 licensed, S3-compatible object storage server that's part of Scality's Zenko project, presenting one AWS S3 interface over backends that can sit on-premises or in public clouds. It runs on Node.js 10.x and yarn 1.17.x, listens on port 8000 with 9990 and 9991 open locally for metadata and data transfer, defaults to the access key `accessKey1` with secret `verySecretKey1` (change both immediately), stores data under `localData` and metadata under `localMetadata`, and ships a Docker image. The repository has around 1,952 stars and dates back to June 2016. Vault-based user management is a separate proprietary component.

## Which route fits your data?

Match the workload, not the marketing.

- **Write once, read rarely, keep for a year or more.** Archive or Coldline storage. Budget the $10.24 per terabyte retrieval fee and accept that a restore is a planned event, not a click.
- **A team that needs file sync, calendars, chat and browser editing.** Self-hosted Nextcloud, with 3–8 GB of RAM set aside for a multi-user Hub deployment.
- **An application that speaks S3 and you don't want vendor lock-in.** Zenko CloudServer on a rented machine, or an S3-compatible service, depending on whether you want to run the daemon.
- **Regulated file sharing with AD/LDAP, 2FA and retention rules.** FileCloud, with S3 or Azure capacity behind it and a licensing conversation you'll need to have with sales.
- **Large, frequently read datasets, or compute sitting next to the data.** A dedicated server. Egress is the reason: at $0.08/GiB, moving data out of a public cloud repeatedly erases the per-gigabyte advantage fast.
- **Under a terabyte, read a few times a year.** Neither a server nor a dedicated box. Standard or Nearline object storage, and no monthly commitment.

The case against each route is worth stating plainly. Self-hosting means you own the monitoring, the capacity planning, the patching and the access controls, and a misconfigured storage resource can hand an outsider full access to your data and account. Renting a server means you also own the durability design, so a single disk with no replication is one failure away from a very bad week. Renting object storage means the bill follows your read patterns, and the cheap tiers are only cheap while you leave the data alone.

## Before you pay

Four things decide whether the invoice matches the plan:

1. **Capacity and how it grows.** A 1 TB NVMe server is a ceiling unless you add drives or move to the 3.84 TB and 7.68 TB configurations. Object storage has no ceiling and no predictability either.
2. **Whether bandwidth is metered.** The dedicated configurations include 30 TB; the KVM plans include 8 TB or 10 TB. Check what happens past the cap before you plan a large restore.
3. **Who handles redundancy and backups.** On a rented server, that's you, and it should be a second location rather than another directory on the same disk.
4. **Billing cycle, renewal and refund terms.** SpinServers bills month to month, publishes a 99.99% uptime SLA, and does not publish a money-back policy, so confirm the terms on the order page before the first payment.

If your data is big, read often, and you'd rather have a fixed line on the balance sheet than a metered one, start with the $79 configuration and scale to the 3.84 TB box when the first terabyte fills up. 👉 [View SpinServers' storage server plans and order the configuration that fits](https://bit.ly/Spinservers)
