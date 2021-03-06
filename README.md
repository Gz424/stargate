
# Stargate upgrade

[Join the Cosmos Stargate announcements channel!](Cosmos Stargate announcements channel!)

If you’re running a block explorer, wallet, exchange, validator, or any other service (eg. custody provider) that depends upon the Cosmos Hub or Cosmos ecosystem, you’ll want to pay attention, because this upgrade will involve substantial changes.

- [Inter-Blockchain Communication (IBC)– cross-chain transactions](https://figment.network/resources/cosmos-stargate-upgrade-overview/#ibc)
- [Protobuf Migration – blockchain performance & dev acceleration](https://figment.network/resources/cosmos-stargate-upgrade-overview/#proto)
- [State Sync – minutes to sync new nodes](https://figment.network/resources/cosmos-stargate-upgrade-overview/#sync)
- [Full-Featured Light Clients](https://figment.network/resources/cosmos-stargate-upgrade-overview/#light)
- [Chain Upgrade Module – upgrade automation](https://figment.network/resources/cosmos-stargate-upgrade-overview/#upgrade)

Help us to get the word out–this is a major leap for the Cosmos Network and we want everyone on board 🚀

## Testnet

We've now launched the Cosmos Hub Stargate testnet `cosmos-hub-stargate` for the Stargate simulated upgrade on October 28, 2020

`cosmos-hub-stargate` is based on Cosmos SDK-0.40-rc1.

The following features are live on the testnet.

* Legacy Amino
* IBC
* State-Sync 
* Cosmovisor


This testnet is intended to be a simulation testnet for Cosmos Hub-3

### Simulated Cosmos Hub-3 Upgrade
A test migration command targeted the blockheight dated around 10/04/2020 for the migration was as follows:

```bash
git clone https://github.com/cosmos/gaia
git checkout cosmos-hub-stargate
make build
```

```
build/gaiad migrate ~/3557667.cosmos_hub_3.json --chain-id=cosmoshub-4 --initial-height 3557668 --replacement-cons-keys ~/iqlusion_work/stargate/validator_replacement.json
```

If you want to reproduce, you may download the Cosmos Hub-3 snapshot here:
[https://storage.googleapis.com/stargate-genesis/3557667.cosmos_hub_3.json](https://storage.googleapis.com/stargate-genesis/3557667.cosmos_hub_3.json)

and the Cosmos Hub-3 genesis snapshot of hub at block height 3557667
[https://storage.googleapis.com/stargate-genesis/snapshot.tgz](https://storage.googleapis.com/stargate-genesis/snapshot.tgz)

This migration command accomplishes the following:
1. Takes the public keys and produces a new validating blockchain

### Stargate-4 Testing
* Testing wallets, exchanges and block explorers against the legacy Amino REST interface
* Giving node operators and validators an opportunity to test their integrations against a work in progress version
* Playing with new Stargate features including IBC is possible now with the Akash realyer! Try it out at https://github.com/ovrclk/relayer/releases/tag/stargate-4


Our validator node for a persistent peer is available at

``` bash
00d8e9c0df367296436854b580d9b069d3f1a5fd@34.123.30.100:26656
```

For users who want to test state sync, our validator node has tendermint rpc open on `34.123.30.100:26657`and we are snapshotting every 1000 blocks.

As of 10/22/2020, the tagged `gaia` version is [stargate-4]()

Remember this version now has a single binary instead of `gaiacli/gaiad` and much more configurable `app.toml`

```bash
git clone https://github.com/cosmos/gaia
git checkout stargate-4
make build
```


## Statesync Configuration Options

State sync rapidly bootstraps a new node by discovering, fetching, and restoring a state machine snapshot from peers instead of fetching and replaying historical blocks. Requires some peers in the network to take and serve state machine snapshots. State sync is not attempted if the node has any local state (LastBlockHeight > 0). The node will have a truncated block history, starting from the height of the snapshot.

In the Tendermint config file there is a state-sync section. Some of these fields must be filled in order to use state-sync.

To find out how to fill in this information please visit: <https://docs.tendermint.com/master/tendermint-core/state-sync.html>

Additionally, some nodes in the network must take state sync snapshots, which are configured in `app.toml`:

Snapshot-interval specifies the block interval at which local state sync snapshots are taken (0 to disable). Must be a multiple of pruning-keep-every.

> NOTE: Please set this value to a non-zero value. This is required in order for other nodes to be able to utilize state-sync.

``` bash
snapshot-interval = {{ .StateSync.SnapshotInterval }}
```

Snapshot-keep-recent specifies the number of recent snapshots to keep and serve (0 to keep all).

``` bash
snapshot-keep-recent = {{ .StateSync.SnapshotKeepRecent }}
```

These are disabled by default, out of caution - this is new code, and we wouldn't want it to cause a chain-wide halt or data corruption. Eventually we can consider enabling them by default.

- [Week 1 Status July 2nd, 2020](week1.md)
- [Week 2 Status July 11th, 2020](week2.md)
- [Week 3 Status July 17th, 2020](week3.md)
- [Week 4 Status July 27th, 2020](week4.md)
- [Week 5 Status August 7th, 2020](week5.md)
- [Week 6 Status August 12th, 2020](week6.md)
- [Week 7 Status August 19th, 2020](week7.md)
- [Week 8 Status August 26th, 2020](week8.md)
- [Week 9 Status September 6th, 2020](week9.md)
- [Week 10 & 11 Status September 16th, 2020](week10_11.md)
- [Week 12 Status September 23, 2020](week12.md)

- [Project Board](https://github.com/orgs/cosmosdevs/projects/1)
