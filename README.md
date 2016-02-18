# cockroachdb-release

Deploy [CockroachDB](https://github.com/cockroachdb/cockroach) easily with this [BOSH](http://docs.cloudfoundry.org/bosh/) release.

## Limitations

* Cockroach is run with `--insecure`
* The gossiping is broken on bosh-lite, probably related to [https://github.com/cloudfoundry/bosh-lite/issues/193](https://github.com/cloudfoundry/bosh-lite/issues/193)

```
gossip/server.go:103: node 1: node 0 believes its address is
10.244.8.10:35016 but that doesn't match any incoming connections:
[[::1]:37801 10.244.8.5:35016]
```

## block_writer

The release includes an errand to run the block_writer example:

```
$ bosh run errand block_writer
```

## Turbulence

[Turbulence](https://github.com/cppforlife/turbulence-release) can be used to check behaviour on node shutdown or network partition.

* You'll need to setup NAT so that the Turbulence API node can talk to the AWS API.
* You can then submit JSON payloads from the `turbulence` subdirectory. For example:

```
curl -vvv -k -X POST https://turbulence:turbulence-password@10.0.1.100:8080/api/v1/incidents -H 'Accept: application/json' -d@turbulence/firewall.json
```

See the [Turbulence API docs](https://github.com/cppforlife/turbulence-release/blob/master/docs/api.md) for more details.

The cockroach team have also been implementing support for testing [CockroachDB correctness with Jepsen](https://github.com/cockroachdb/jepsen).
