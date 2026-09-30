# Ceph & Distributed Storage

Notes from building and running a real Ceph cluster on my own time, since I wanted to understand distributed storage from the inside rather than just reading about it. Along the way this turned into 7 open pull requests against `ceph/ceph`.

📖 **Full write-up:** [index.md](index.md)

## Along the way

- **[PR #71923](https://github.com/ceph/ceph/pull/71923)**: squid Grafana certificate fix for long FQDNs, with tests, own discovery
- **[PR #71407](https://github.com/ceph/ceph/pull/71407)**: cephadm certificate hardening, with tests (first attempt at the fix above)
- **[PR #71409](https://github.com/ceph/ceph/pull/71409)**: cephadm timezone bug fix, with tests, verified from a report
- **[PR #71410](https://github.com/ceph/ceph/pull/71410)**: OSD drain timestamp fix, with tests, verified from a report
- **[PR #71413](https://github.com/ceph/ceph/pull/71413)**: Prometheus metrics fix, with tests, verified from a report
- **[PR #71757](https://github.com/ceph/ceph/pull/71757)**: RGW multi-zone create fix, with tests
- **[PR #71405](https://github.com/ceph/ceph/pull/71405)**: documentation contribution to `ceph/ceph`

## Start here

→ [ceph-handson](https://joshjan20.github.io/ceph-handson/)
