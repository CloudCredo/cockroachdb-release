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
