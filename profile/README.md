# BCH CoinJoin

This GitHub group hold code repositories that are used to build a desktop application for generating [CoinJoin transactions](https://en.bitcoin.it/wiki/CoinJoin) on the Bitcoin Cash (BCH) blockchain. The work to create this code was funding by a [Flipstarter](https://flipstarter.cash/) campaign, which will fund work from January 1st 2023 until April 1st 2023. [Updates on progress are posted here.](https://gist.github.com/christroutner/da18dabfcb3daf75e8d11d400753f29a)

There are five design elements that go into a desktop application for generating CoinJoin transactions:

- Packaging - This is the desktop app using Electron.js. It will be compiled and tested on Windows, Mac, and Linux. The UI will closely resemble [wallet.FullStack.cash](https://bchn-wallet.fullstack.cash).
- Back End Infrastructure - this part is complete for the most part. It will use the [web3 Cash Stack](https://cashstack.info/).
- HD wallet functionality - this part is mostly complete. The code exists in [slp-cli-wallet](https://github.com/Permissionless-Software-Foundation/slp-cli-wallet), which is an older project. The code needs to be dusted off and customized for this app. The HD address tracking needs to be slightly refined.
- p2p coordination - The bulk of this code is complete. The [ipfs-coord](https://www.npmjs.com/package/ipfs-coord) library will be leveraged, and adapted to fit the [Collaborative CoinJoin protocol](https://github.com/Permissionless-Software-Foundation/specifications/blob/master/ps004-collaborative-coinjoin.md).
- CoinJoin protocol - [The Collaborative CoinJoin protocol](https://github.com/Permissionless-Software-Foundation/specifications/blob/master/ps004-collaborative-coinjoin.md) will be developed and adapted from [this CoinJoin code example](https://github.com/Permissionless-Software-Foundation/psf-js-examples/tree/master/bch-js/bch/applications/collaborate/coinjoin). But the code will be developed in a modular fashion, so that it can be swapped out with additional protocols in the future. This will allow better (but harder to develop) CoinJoin protocols like [CashShuffle](https://github.com/cashshuffle/spec) and [CashFusion](https://cashfusion.org/) to be swapped in later, without having to change the other four design elements.

## Repoistories

Here is a list of the repositories in this GitHub Group:

- [electron-bch-wallet-single-addr](https://github.com/bch-coinjoin/electron-bch-wallet-single-addr) is a boilerplate [Electron.js](https://www.electronjs.org/) desktop app. This is not the final desktop app, but is instead a boilerplate. The final desktop app will be forked from this repository. It contains a single-address wallet, the same that is used by [wallet.fullstack.cash](https://wallet.fullstack.cash), and is generated from the code in the [bch-wallet-web3-android](https://github.com/Permissionless-Software-Foundation/bch-wallet-web3-android) code repository.
