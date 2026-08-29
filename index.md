# Ceph & Distributed Storage

## Why I Started This

I come from a software and infrastructure automation background, hands-on with AWS, Ansible at scale, and reliability-critical systems. What pulled me toward Ceph specifically was a simple question I couldn't stop thinking about: when AWS S3 advertises 99.999999999% durability, what does that actually mean, mechanically? Not as a marketing number, but as a system you could build, break, and watch recover.

So I built one. A real 3-node Ceph cluster, from scratch, on my own infrastructure. Once it was running, I kept finding more worth digging into: what happens when a node actually dies, why a certificate was silently failing, how to see the cluster's health at a glance instead of squinting at terminal output, how it performs under load. A few of those threads led further than I expected, including two pull requests I ended up opening against `ceph/ceph` itself.

This page links to that work as it stands. Each project below is documented as I actually did it, real command output, real screenshots, and in two cases, live pull requests still working their way through review.

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
| 6 | [ceph-maintenance-tool](https://joshjan20.github.io/ceph-maintenance-tool/) | A real Python maintenance/debugging tool: structured exit codes, `--quiet` mode for cron, JSON output |
| 7 | [ceph-doc-contribution](https://joshjan20.github.io/ceph-doc-contribution/) | **[PR #71405](https://github.com/ceph/ceph/pull/71405)**: a documentation contribution filling a real gap between RGW deployment and S3 client usage |
| 8 | [ceph-benchmarking](https://joshjan20.github.io/ceph-benchmarking/) | Performance benchmarking (throughput vs. IOPS, large vs. small objects) with a generated, self-contained HTML dashboard |
| 9 | [ceph-ansible](https://joshjan20.github.io/ceph-ansible/) | Automating cluster tooling deployment with an idempotent Ansible playbook, verified via dry-run and repeat-run testing |
| 10 | [ceph-code-fix](https://joshjan20.github.io/ceph-code-fix/) | **[PR #71407](https://github.com/ceph/ceph/pull/71407)**: the actual code fix (with regression tests) for the bug diagnosed in Part 3 |

---

## Upstream Contributions

- **[PR #71405](https://github.com/ceph/ceph/pull/71405)**: RGW + AWS CLI quickstart documentation
- **[PR #71407](https://github.com/ceph/ceph/pull/71407)**: cephadm certificate generation fix (X.509 Common Name length limit), with unit tests
- Bug report submitted via Ceph's official issue tracker (see [Part 5](https://joshjan20.github.io/ceph-tracker-report/) for status)

---

## Technical Coverage

- **Cluster operations:** cephadm, bootstrapping, OSD management, RADOS Gateway (S3-compatible object storage)
- **Reliability:** replication behavior, failure simulation, self-healing, degraded-state operation
- **Observability:** Grafana, Prometheus, alerting rules and state machines
- **Automation:** Ansible (idempotent playbooks), Python tooling
- **Performance:** `rados bench`, throughput vs. IOPS analysis, dashboard generation
- **Community:** issue tracker engagement, documentation and code contributions to `ceph/ceph`

---

*Contact: j.samuel.tec@gmail.com*
