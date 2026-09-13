# Coffey Labs

Open-source infrastructure — mail, observability, VPN, and the systems
tooling around them. **Copyleft-licensed without exception:** every project here is
GPLv3 or AGPLv3, including the parts other projects would hold back.

🌐 [coffeylabs.org](https://coffeylabs.org)

---

## Projects

### 📬 [ihasmail](https://github.com/Coffey-Labs/ihasmail) &nbsp;·&nbsp; TypeScript &nbsp;·&nbsp; AGPL-3.0

**Immutable webmail for [Stalwart Mail Server](https://stalw.art).**

A Gmail-class single-page client — mail, calendars, contacts, files and Sieve
filters — that speaks only JMAP. No IMAP, no SMTP, no database, and with
`IMMUTABLE=1` no writable filesystem either: everything durable belongs to
Stalwart, and the container is disposable. Settings live in the account's own
JMAP Files rather than the browser, so the app itself stays stateless.

Three-pane conversation view with Gmail search operators and shortcuts, a
recurrence- and free-busy-aware calendar, vCard import/export, an installable
PWA with Web Push, and nine interface languages beyond English. Requires
Stalwart 0.16 or newer.

[Live demo](https://demo.ihasmail.com) · [ihasmail.org](https://ihasmail.org) · [docs.ihasmail.org](https://docs.ihasmail.org)

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

---

### 📊 [cairnobs](https://github.com/Coffey-Labs/cairnobs) &nbsp;·&nbsp; Go + Rust &nbsp;·&nbsp; AGPL-3.0

**Open-core, Kubernetes-native log aggregation and observability.**

Built to match Splunk on capability while winning on cost-per-GB, with honest
multi-tenant RBAC. Logs flow from a statically-linked Rust edge agent through
Redpanda into a Go ingest pipeline, landing in ClickHouse for analytics and
Tantivy for full-text search — one query language spanning both stores,
compiling to a single execution plan, with raw ClickHouse SQL as an escape
hatch onto the same IR.

On top: dashboards, a threshold-and-absence alerting evaluator, a `cairnobsctl`
CLI, a Terraform provider, and AI-assisted query authoring that runs against a
self-hosted Ollama model by default. Ships as a Kubernetes Operator, Helm chart
or docker-compose. The `enterprise/` directory is AGPLv3 like everything else.

[cairnobs.org](https://cairnobs.org)

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

| Project | Licence |
|---|---|
| ihasmail | AGPL-3.0-or-later |
| ihasvpn | AGPL-3.0-or-later |
| cairnobs | AGPL-3.0-or-later (including `enterprise/`) |
| stalwart-migrator | GPL-3.0 |
| SysAdminAutomation | GPL-3.0 |
| ubuntu2mint | GPL-3.0 |

Copyleft without exception — no open-core carve-outs, no source-available
licences, no relicensed "enterprise" tier.
