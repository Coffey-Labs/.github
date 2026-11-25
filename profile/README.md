# Coffey Labs

Open-source infrastructure — mail, monitoring, VPN, websites, and the
systems tooling around them. **Copyleft-licensed without exception:** every project here is
GPLv3 or AGPLv3, including the parts other projects would hold back.

🌐 [coffeylabs.org](https://coffeylabs.org) &nbsp;·&nbsp; also at [@inbuxa](https://github.com/inbuxa)

---

## Projects

### 📦 [inbuxa](https://github.com/inbuxa) &nbsp;·&nbsp; Rust + TypeScript &nbsp;·&nbsp; AGPL-3.0

**A complete mail system you run yourself** — the server, its administration
console and its webmail, installed and versioned together, with every feature
in the one edition and no license key anywhere in the code.

Built here, but kept in **[its own organization](https://github.com/inbuxa)**:
it is several repositories that ship as one thing, and they belong next to each
other rather than scattered through this list. Same people, same license, same
rule about no gated features.

[inbuxa.org](https://inbuxa.org) · [docs.inbuxa.org](https://docs.inbuxa.org) · [github.com/inbuxa](https://github.com/inbuxa)

---

### 📬 [ihasmail](https://github.com/Coffey-Labs/ihasmail) &nbsp;·&nbsp; TypeScript &nbsp;·&nbsp; AGPL-3.0

**Immutable webmail for [Stalwart Mail Server](https://stalw.art).**

A Gmail-class single-page client — mail, calendars, contacts, files and Sieve
filters — that speaks only JMAP. No IMAP, no SMTP, no database, and with
`IMMUTABLE=1` no writable filesystem either: everything durable belongs to
Stalwart, and the container is disposable. Settings live in the account's own
JMAP Files rather than the browser, so the app itself stays stateless.

Three-pane conversation view with Gmail search operators and shortcuts, a
recurrence- and free-busy-aware calendar, vCard import/export, an installable
PWA with Web Push, and a translated interface. Requires Stalwart 0.16 or newer.

[Live demo](https://demo.inbuxa.org) · [ihasmail.org](https://ihasmail.org) · [docs.ihasmail.org](https://docs.ihasmail.org)

---

### 🔐 [ihasvpn](https://github.com/Coffey-Labs/ihasvpn) &nbsp;·&nbsp; Go + TypeScript &nbsp;·&nbsp; AGPL-3.0

**A self-hosted WireGuard server with a secure web console, in one container.**

Peers with QR codes and `.conf` downloads, who is connected and how much they
move, disconnect and session reset with a click, key rotation, expiry, and
client-supplied keys for devices that keep their own. The tunnel runs on the
kernel's WireGuard module over netlink, with nftables NAT, TCP MSS clamping and
tuned sysctls, so it goes as fast as the host allows; wireguard-go is the
fallback where the module is missing. argon2id passwords, two-factor with
recovery codes, viewer and administrator roles, an audit log and Prometheus
metrics. One static binary and one SQLite file; nothing else to run.

[ihasvpn.org](https://ihasvpn.org)

---

### 📊 [Cairn OBS](https://github.com/Coffey-Labs/cairnobs) &nbsp;·&nbsp; Go + Svelte &nbsp;·&nbsp; AGPL-3.0

**Self-hosted monitoring for networks, hosts, services and clusters.**

An agent on each host reports to one server, which judges the readings, draws
the maps from what is actually running, sends the alerts and writes the
reports. It reads and never changes anything, and it runs on your own
hardware, from a single container to a cluster watching thousands of VMs and
pods. Hosts, checks, clusters, hypervisors, storage arrays, IBM i and Windows
servers, with nothing held back for a paid tier.

[cairnobs.org](https://cairnobs.org) · [Live demo](https://demo.cairnobs.org) · [docs.cairnobs.org](https://docs.cairnobs.org)

---

### 🌭 [HotDog CMS](https://github.com/Coffey-Labs/hotdog-cms) &nbsp;·&nbsp; Go &nbsp;·&nbsp; AGPL-3.0

**A website builder: write in Markdown, see it live, publish from git.**

For people who want a fast, safe site without babysitting a server. Pages are
plain files, every change is a commit, and the public site is nothing but
pages. The editor previews as you type and works with any git platform; the
build publishes anywhere static files can be served. The Coffey Labs sites
run on it.

[hotdogcms.org](https://hotdogcms.org) · [Docs](https://hotdogcms.org/docs/)

---

### 🚀 [ihasmail-oneshot](https://github.com/Coffey-Labs/ihasmail-oneshot) &nbsp;·&nbsp; Go &nbsp;·&nbsp; AGPL-3.0

**One command that turns a Linux Docker host into a working mail server with
webmail.**

Deploys a fresh Stalwart and a fresh ihasmail behind Caddy, links them, gets
them certificates, and hands you the administrator password and the DNS records
to publish. Along the way it completes Stalwart's bootstrap through its API
without leaving the one-time credential behind, gives Stalwart its own ACME
account so it doesn't fight Caddy for port 443, and stops one scanning bot from
getting the proxy banned for everyone. It checks the host before changing
anything and proves the link by signing in through the webmail before calling
itself done.

A single static binary for amd64 and arm64, standard library only. `--local`
gives a loopback-only stack for trying ihasmail against a real Stalwart; what
it leaves behind is an ordinary `docker compose` project, not tied to the tool.

[Releases](https://github.com/Coffey-Labs/ihasmail-oneshot/releases/latest)

---

### 🔧 [stalwart-migrator](https://github.com/Coffey-Labs/stalwart-migrator) &nbsp;·&nbsp; Go &nbsp;·&nbsp; GPL-3.0

**In-place upgrade tooling for Stalwart Mail Server, 0.15.5 → latest.**

A checkpoint at every step, so an interrupted run resumes instead of
restarting, plus automated validation that the server still works afterwards.
Go, standard library only — no external dependencies.

Used in production: a live nine-domain, 2.4 GB RocksDB server went 0.15.5 →
0.16.19 with 8 seconds of downtime, every phase green. An independent user has
since reported runs at roughly 221 GB across 16 domains and 55 accounts.
Preflight refuses on the two things it cannot fix for you — shared-tenant
domains, and migrating as the built-in fallback admin. Recovery from a failed
migration is your own snapshot; this tool does not undo one.

---

### 🛠 [SysAdminAutomation](https://github.com/Coffey-Labs/SysAdminAutomation) &nbsp;·&nbsp; Shell &nbsp;·&nbsp; GPL-3.0

**Fifteen Bash scripts for routine Linux administration** — backups, log
handling, monitoring, user and service management, package updates.

Distribution-agnostic, using only base utilities, each carrying its usage in
its header. The conventions are consistent across the collection: `--dry-run`
changes nothing, anything destructive confirms first, `--yes` / `ASSUME_YES=1`
skips the prompt for unattended use — and with no tty and no override, a
destructive script **refuses** rather than guessing. All fifteen run under
`set -euo pipefail` and are ShellCheck-linted on every push.

---

### 🖥 [ubuntu2mint](https://github.com/Coffey-Labs/ubuntu2mint) &nbsp;·&nbsp; Shell &nbsp;·&nbsp; GPL-3.0

**High-risk, best-effort in-place conversion of Ubuntu toward Linux Mint** —
Ubuntu stays the base OS while Mint repositories, desktop and tooling are added
on top, approximating Mint without a reinstall.

Supports Ubuntu 24.04 → Mint 22.x and 22.04 → Mint 21.x, with conservative APT
pinning, lock detection, a pre-install simulation that aborts on critical-package
removal, and backup/rollback support. A second script prunes the leftover Ubuntu
GNOME desktop *after* you have booted a working Mint session.

Unsupported by design and gated behind both an interactive acknowledgement and
`--i-accept-the-risk`. EDR/MDM/VPN tooling may break; a clean install is the
recommended path. For experienced admins who understand APT pinning, display
managers and rollback.

---

## Licensing

| Project | License |
|---|---|
| ihasmail | AGPL-3.0-or-later |
| ihasvpn | AGPL-3.0-or-later |
| Cairn OBS | AGPL-3.0 |
| HotDog CMS | AGPL-3.0-or-later |
| ihasmail-oneshot | AGPL-3.0-or-later |
| stalwart-migrator | GPL-3.0 |
| SysAdminAutomation | GPL-3.0 |
| ubuntu2mint | GPL-3.0 |

The [inbuxa](https://github.com/inbuxa) repositories are AGPL-3.0 too, and
carry their own table in that organization's profile.

Copyleft without exception — no open-core carve-outs, no source-available
licenses, no relicensed "enterprise" tier.
