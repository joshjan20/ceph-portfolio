# Ceph & Distributed Storage

## Why I Started This

I come from a software and infrastructure automation background, hands-on with AWS, Ansible at scale, and reliability-critical systems. What pulled me toward Ceph specifically was a simple question I couldn't stop thinking about: when AWS S3 advertises 99.999999999% durability, what does that actually mean, mechanically? Not as a marketing number, but as a system you could build, break, and watch recover.

So I built one. A real 3-node Ceph cluster, from scratch, on my own infrastructure. Once it was running, I kept finding more worth digging into: what happens when a node actually dies, why a certificate was silently failing, how to see the cluster's health at a glance instead of squinting at terminal output, how it performs under load. A few of those threads led further than I expected, including 5 pull requests I've now opened against `ceph/ceph` itself, four code fixes with regression tests and one documentation contribution.

This page links to that work as it stands. Each project below is documented as I actually did it, real command output, real screenshots, and in several cases, live pull requests still working their way through review.

I'm particularly interested in the operational side of distributed storage at scale: how systems like Ceph get run reliably across large clusters and multiple data centers, the tooling and automation that makes that sustainable, and the open-source community that maintains it. That's the direction I want to keep learning in.

---

## What's Here

| # | Project | What it covers |
|---|---|---|
| 1 | [ceph-handson](https://joshjan20.github.io/ceph-handson/) | Building a 3-node Ceph cluster from scratch: cephadm, bootstrapping, OSDs, RADOS Gateway, and real setup troubleshooting (7 documented gotchas) |
| 2 | [ceph-self-healing](https://joshjan20.github.io/ceph-self-healing/) | Simulating a node failure on purpose and watching the cluster detect, degrade gracefully, keep serving data, and self-heal on recovery |
| 3 | [ceph-grafana](https://joshjan20.github.io/ceph-grafana/) | Diagnosing a real cephadm certificate bug down to the exact root cause, fixing it locally, and visualizing the cluster |
| 4 | [ceph-alerting](https://joshjan20.github.io/ceph-alerting/) | Building and triggering a real automated Grafana alert, with a timestamped state-machine trace (Normal → Pending → Alerting) |
| 5 | [ceph-tracker-report](https://joshjan20.github.io/ceph-tracker-report/) | Reporting the Part 3 bug through Ceph's official issue tracker, including the real account-activation friction involved |
| 6 | [ceph-maintenance-tool](https://github.com/joshjan20/ceph-maintenance-tool) | A real Python maintenance/debugging tool: structured exit codes, `--quiet` mode for cron, JSON output |
| 7 | [ceph-rgw-docs](https://joshjan20.github.io/ceph-rgw-docs/) | **[PR #71405](https://github.com/ceph/ceph/pull/71405)**: a documentation contribution filling a real gap between RGW deployment and S3 client usage |
| 8 | [ceph-benchmarking](https://joshjan20.github.io/ceph-benchmarking/) | Performance benchmarking (throughput vs. IOPS, large vs. small objects) with a generated, self-contained HTML dashboard |
| 9 | [ceph-ansible-automation](https://joshjan20.github.io/ceph-ansible-automation/) | Automating cluster tooling deployment with an idempotent Ansible playbook, verified via dry-run and repeat-run testing |
| 10 | [ceph-code-fix](https://joshjan20.github.io/ceph-code-fix/) | **[PR #71407](https://github.com/ceph/ceph/pull/71407)**: the actual code fix (with regression tests) for the bug diagnosed in Part 3 |
| 11 | [ceph-timezone-fix](https://joshjan20.github.io/ceph-timezone-fix/) | **[PR #71409](https://github.com/ceph/ceph/pull/71409)**: verifying and fixing a timezone bug in certificate expiry checks, reported by someone else and confirmed independently before acting on it |
| 12 | [ceph-osd-drain-timestamp-fix](https://joshjan20.github.io/ceph-osd-drain-timestamp-fix/) | **[PR #71410](https://github.com/ceph/ceph/pull/71410)**: a related timezone/serialization bug in OSD drain timestamps, reconstructed and verified from a partially garbled report |
| 13 | [ceph-prometheus-rgw-fix](https://joshjan20.github.io/ceph-prometheus-rgw-fix/) | **[PR #71413](https://github.com/ceph/ceph/pull/71413)**: a guard-condition/indexing mismatch in Prometheus metrics collection that could silently break cluster-wide metrics over one oddly-named RGW daemon |

---

## Upstream Contributions

- **[PR #71407](https://github.com/ceph/ceph/pull/71407)**: cephadm certificate generation fix (X.509 Common Name length limit), with unit tests, own discovery
- **[PR #71409](https://github.com/ceph/ceph/pull/71409)**: cephadm certificate expiry timezone fix, with unit tests, verified from someone else's report (tracker [#80928](https://tracker.ceph.com/issues/80928))
- **[PR #71410](https://github.com/ceph/ceph/pull/71410)**: OSD drain timestamp timezone/serialization fix, with unit tests, verified from a partially garbled report (tracker [#80929](https://tracker.ceph.com/issues/80929))
- **[PR #71413](https://github.com/ceph/ceph/pull/71413)**: Prometheus RGW metrics IndexError fix, with unit tests, verified from a detailed report (tracker [#80930](https://tracker.ceph.com/issues/80930)). Under upstream review: a Ceph developer reproduced the bug on a live cluster and confirmed the fix resolves it
- **[PR #71405](https://github.com/ceph/ceph/pull/71405)**: RGW + AWS CLI quickstart documentation
- Bug report submitted via Ceph's official issue tracker (see [Part 5](https://joshjan20.github.io/ceph-tracker-report/) for status)

---

## Technical Coverage

- **Cluster operations:** cephadm, bootstrapping, OSD management, RADOS Gateway (S3-compatible object storage)
- **Reliability:** replication behavior, failure simulation, self-healing, degraded-state operation
- **Observability:** Grafana, Prometheus, alerting rules and state machines
- **Automation:** Ansible (idempotent playbooks), Python tooling
- **Performance:** `rados bench`, throughput vs. IOPS analysis, dashboard generation
- **Debugging:** verifying bug reports against real source before trusting them, reproducing failures with real code, root-causing across cephadm and Prometheus subsystems
- **Community:** issue tracker engagement, documentation and code contributions to `ceph/ceph`

---

*Contact: j.samuel.tec@gmail.com*
