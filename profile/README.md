# BCH CoinJoin

This GitHub group holds code repositories that are used to build a desktop application for generating [CoinJoin transactions](https://en.bitcoin.it/wiki/CoinJoin) on the Bitcoin Cash (BCH) blockchain. The work to create this code was funded by a [Flipstarter](https://flipstarter.cash/) campaign, which will fund work from January 1st 2023 until April 1st 2023. [Updates on progress are posted here.](https://gist.github.com/christroutner/da18dabfcb3daf75e8d11d400753f29a)

There are *five design elements* that go into a desktop application for generating CoinJoin transactions:

1. **Packaging** - This is the desktop app using [Electron.js](https://www.electronjs.org/). It will be compiled and tested on Windows, Mac, and Linux. The UI will closely resemble [wallet.FullStack.cash](https://bchn-wallet.fullstack.cash).
2. **Back End Infrastructure** - this part is complete for the most part. It will use the [web3 Cash Stack](https://cashstack.info/).
3. **HD wallet functionality** - this part is mostly complete. The code exists in [slp-cli-wallet](https://github.com/Permissionless-Software-Foundation/slp-cli-wallet), which is an older project. The code needs to be dusted off and customized for this app. The HD address tracking needs to be slightly refined.
4. **p2p coordination** - The bulk of this code is complete. The [ipfs-coord](https://www.npmjs.com/package/ipfs-coord) library will be leveraged, and adapted to fit the [Collaborative CoinJoin protocol](https://github.com/Permissionless-Software-Foundation/specifications/blob/master/ps004-collaborative-coinjoin.md).
5. **CoinJoin protocol** - [The Collaborative CoinJoin protocol](https://github.com/Permissionless-Software-Foundation/specifications/blob/master/ps004-collaborative-coinjoin.md) will be developed and adapted from [this CoinJoin code example](https://github.com/Permissionless-Software-Foundation/psf-js-examples/tree/master/bch-js/bch/applications/collaborate/coinjoin). But the code will be developed in a modular fashion, so that it can be swapped out with additional protocols in the future. This will allow better (but harder to develop) CoinJoin protocols like [CashShuffle](https://github.com/cashshuffle/spec) and [CashFusion](https://cashfusion.org/) to be swapped in later, without having to change the other four design elements.

## Repositories

Here is a list of the repositories in this GitHub Group:

- [electron-bch-wallet-single-addr](https://github.com/bch-coinjoin/electron-bch-wallet-single-addr) is a boilerplate [Electron.js](https://www.electronjs.org/) desktop app. This is not the final desktop app, but is instead a boilerplate. It is not directly used in this project. The final desktop app will be forked from this repository. It contains a single-address wallet, the same that is used by [wallet.fullstack.cash](https://wallet.fullstack.cash), and is generated from the code in the [bch-wallet-web3-android](https://github.com/Permissionless-Software-Foundation/bch-wallet-web3-android) code repository.

- [electron-bch-coinjoin-wallet](https://github.com/bch-coinjoin/electron-bch-coinjoin-wallet) is an Electron.js desktop app forked from the repository above. This *is* the final desktop app. In addition to the desktop user interface, it includes an embedded copy of [go-ipfs](https://ipfs.io) for p2p communication, and a copy of colab-coinjoin-api as a back-end REST API.

- [colab-coinjoin-api](https://github.com/bch-coinjoin/colab-coinjoin-api) is a REST API server. It is embedded in electron-bch-coinjoin-wallet, or it can be operated as a stand-alone webserver. It spins up a go-ipfs node at startup, to provide p2p communication. It also provides a REST API for the front web UI and the command-line wallet.

- [hd-cli-wallet](https://github.com/bch-coinjoin/hd-cli-wallet) is the HD wallet 'engine'. This library can create new wallets, manage UTXOs within an HD wallet context, and send BCH and tokens. It communicates with the colab-coinjoin-api REST API in order to consolidate UTXOs through CoinJoin. It provides a command-line interface (CLI) for developers, and it also exports its functionality into an npm library that is compiled for use in a web browser UI. That library is used by the electron-bch-coinjoin-wallet user interface.
