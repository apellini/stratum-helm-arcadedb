# stratum-helm-arcadedb

Minimal Helm chart wrapping the official [ArcadeDB](https://arcadedb.com) graph database
for the STRATUM platform. ArcadeDB is the primary graph store for the Specter digital twin
module (all modules access the topology graph via Specter's Graph Query API).

## Usage

```bash
helm repo add apellini-arcadedb https://apellini.github.io/stratum-helm-arcadedb
helm install arcadedb apellini-arcadedb/arcadedb --namespace stratum-data
```

## Configuration

| Parameter | Description | Default |
|-----------|-------------|---------|
| `replicaCount` | Number of replicas (1 for dev; 3 for prod Raft cluster) | `1` |
| `image.tag` | ArcadeDB image tag (defaults to Chart.AppVersion) | `""` |
| `persistence.size` | PVC size | `50Gi` |
| `javaOpts` | JVM options | `-Xms1g -Xmx3g` |
| `resources.limits.memory` | Memory limit | `4Gi` |
| `service.httpPort` | HTTP/REST API port | `2480` |
| `service.binaryPort` | Binary protocol port | `2424` |

## Ports

| Port | Protocol | Description |
|------|----------|-------------|
| 2480 | HTTP | REST API — used by all STRATUM control-plane services |
| 2424 | TCP | Binary protocol |

## Production (Raft cluster)

Set `replicaCount: 3` for the 3-node Raft cluster defined in the Specter LLD. Each replica
gets its own PVC via `volumeClaimTemplates`.

## License

Apache 2.0 — see [LICENSE](LICENSE).
