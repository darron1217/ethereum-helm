
# ethereum-node

![Version: 0.0.16](https://img.shields.io/badge/Version-0.0.16-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)

This chart acts as an umbrella chart and allows to run a ethereum execution and consensus layer client. It's also able to deploy optional monitoring applications.

**Homepage:** <https://ethereum.org>

## Source Code

* <https://github.com/ethpandaops/ethereum-helm-charts>

## Subcharts
| Repository | Name | Version |
|------------|------|---------|
| file://../geth | geth | 1.0.7 |
| file://../lighthouse | lighthouse | 1.1.1 |
| file://../nethermind | nethermind | 1.0.9 |
| file://../teku | teku | 1.1.1 |

# Details

Ideally you should have a look at the default [values.yaml](values.yaml) to get a better understanding on how this chart works.

### Pre-defined networks

The following networks are built into the chart and can be configured by just setting the `global.main.network` variable:

- mainnet
- goerli

### Consensus layer checkpoint sync

The chart also has pre-defined checkpoint sync endpoints for each one of the built in networks. By default, the chart will be using these. You can disable this by setting `global.checkpointSync` to `false`.

```yaml
global:
  checkpointSync:
    enabled: true
    addresses:
      mainnet: https://mainnet-checkpoint-sync.attestant.io
      goerli: https://checkpoint-sync.goerli.ethpandaops.io
```

### Choosing the execution and consensus layer software

For the consensus layer node, you can choose between lighthouse, lodestar, teku, prysm or lighthouse. To enable one of them, you'll need to set the clients `enabled` var to `true`. For example:

```yaml
lighthouse:
  enabled: true
```

For the execution layer node you can choose between besu, ,erigon, geth or nethermind. To enable one of them you follow the same approach as before:

```yaml
geth:
  enabled: true
```

*Note:* You should not enable multiple CL/EL nodes. The chart only works if you enable 1 EL and 1 CL node.

# Complete example

Run lighthouse/geth combo on the Goerli network with metrics-exporter enabled:

```yaml
##
## $ helm install goerli-lighthouse-geth-0 ethereum-helm-charts/ethereum-node -f values.yaml
##

global:
  main:
    network: goerli
  checkpointSync:
    enabled: true

# Client pairs
geth:
  enabled: true
lighthouse:
  enabled: true
```
