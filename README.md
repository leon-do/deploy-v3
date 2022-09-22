# Deploy Uniswap V3 Script

This package includes a CLI script for deploying the latest Uniswap V3 smart contracts to any EVM (Ethereum Virtual Machine) compatible network.

## Licensing

Please note that Uniswap V3 is under [BUSL license](https://github.com/Uniswap/v3-core#licensing) until the Change Date, currently 2023-04-01. Exceptions to the license may be specified by Uniswap Governance via Additional Use Grants, which can, for example, allow V3 to be deployed on new chains. Please follow the [Uniswap Governance process](https://gov.uniswap.org/t/community-governance-process/7732) to request a DAO vote for exceptions to the license, or to move up the Change Date.

License changes must be enacted via the [ENS domain](https://ens.domains/) uniswap.eth, which is controlled by Uniswap Governance. This means (among other things) that Governance has the power to associate arbitrary text with any subdomain of the form X.uniswap.eth. Modifications of the Change Date should be specified at v3-core-license-date.uniswap.eth, and Additional Use Grants should be specified at v3-core-license-grants.uniswap.eth. The process for associating text with a subdomain is detailed below:

1. If the subdomain does not already exist (which can be [checked at this URL](https://app.ens.domains/name/uniswap.eth/subdomains)), the [`setSubnodeRecord`](https://docs.ens.domains/contract-api-reference/ens#set-subdomain-record) function of the ENS registry should be called with the following arguments:

- `node`: `namehash('uniswap.eth')` (`0xa2a03459171c76bff45817330c10ef9f8af07011a33005b73b50189bbc7e7132`)
- `label`: `keccak256('v3-core-license-date')` (`0xee55740591b0fd5d7a28a6edc49567f6ff3febbe942ec0e2fa49ee536595085b`) or `keccak256('v3-core-license-grants')` (`0x15ff9b5bd7642701a10e5ea8fb29c957ffda4854cd028e9f6218506e6b509af2`)
- `owner`: [`0x1a9C8182C09F50C8318d769245beA52c32BE35BC`](https://etherscan.io/address/0x1a9c8182c09f50c8318d769245bea52c32be35bc), the Uniswap Governance Timelock
- `resolver`: [`0x4976fb03c32e5b8cfe2b6ccb31c09ba78ebaba41`](https://etherscan.io/address/0x4976fb03c32e5b8cfe2b6ccb31c09ba78ebaba41), the public ENS resolver.
- `ttl`: `0`

2. Then, the [`setText`](https://docs.ens.domains/contract-api-reference/publicresolver#set-text-data) function of the public resolver should be called with the following arguments:

- `node`: `namehash('v3-core-license-date.uniswap.eth')` (`0x0505ec7822d61b4cfb294f137d1a7f0ceedf162f555a4bf2f4be58a07cf266c5`) or `namehash('v3-core-license-grants.uniswap.eth')` (`0xa35d592ec6e5289a387cba1d5f82be794f495bd5a361a1fb314687c6aefea1f4`)
- `key`: A suitable label, such as `notice`.
- `value`: The text of the change. Note that text may already be associated with the subdomain in question. If it does, it can be reviewed at the following URLs for either [v3-core-license-date](https://app.ens.domains/name/v3-core-license-date.uniswap.eth/details) or [v3-core-license-grants](https://app.ens.domains/name/v3-core-license-grants.uniswap.eth/details), and appended to as desired.

Note: [`setContentHash`](https://docs.ens.domains/contract-api-reference/publicresolver#set-content-hash) may also be used to associate text with a subdomain, but `setText` is presented above for simplicity.

These contract function calls should ultimately be encoded into a governance proposal, about which more details are available [here](https://docs.uniswap.org/protocol/concepts/governance/overview).

## Setup

`yarn`

`yarn build`

`node dist/index.js --help`

```
node dist/index.js \
--private-key 0x37635c4151472cee730470bf25c92ce368939dcb130c67f751403eb3f8ab66ff \
--json-rpc https://rpc.ankr.com/eth_goerli \
--weth9-address 0xb4fbf271143f4fbf7b91a5ded31805e42b2208d6 \
--native-currency-label gETH \
--owner-address 0x0af409ef995f90758470883aefe220b3caf853c6
```

```
Step 1 complete [
  {
    message: 'Contract UniswapV3Factory deployed',
    address: '0x7dEe2742F95516023Ea772e76eF42F15C94233F6',
    hash: '0xd0ea6ae81d854aebc6152f9c2e35eeaaf2b9823522bf33b31d0cab24f1410d63'
  }
]
Step 2 complete [
  {
    message: 'UniswapV3Factory added a new fee tier 1 bps with tick spacing 1',
    hash: '0x66ee755b5c9cd96ac6029ad316dd0c829b3fce230ba5421a9e711c383df5e9b6'
  }
]
Step 3 complete [
  {
    message: 'Contract UniswapInterfaceMulticall deployed',
    address: '0x3EEd5a7fAd89C3BA937f7Bc43d2097E7C351b8E3',
    hash: '0x881356a2a0f272593e055df7b9e06a5fe60573ff816753705013e48039d096f4'
  }
]
Step 4 complete [
  {
    message: 'Contract ProxyAdmin deployed',
    address: '0x95CC6A7Ee69dB956692f8639b9B2FF5C20Cd046A',
    hash: '0xfc282ea62b3dca4a7debfb82df61aca3b8c1916a300a69101630e4194a790834'
  }
]
Step 5 complete [
  {
    message: 'Contract TickLens deployed',
    address: '0x9DACFb107BC91F11234b62A82553f318cf0010b4',
    hash: '0x49dfad51c30469ff002e1ecf9abfa8deaa04a0da2159ea48ccb051754ee6fd77'
  }
]
Step 6 complete [
  {
    message: 'Library NFTDescriptor deployed',
    address: '0x2A62BAf93A771dF1aA719edFdBE906F8271faa0E',
    hash: '0x5faead41ad23bcb59d298f8b86c232179e44d27a5bc01831a56a8f4c35cafccc'
  }
]
Step 7 complete [
  {
    message: 'Contract NonfungibleTokenPositionDescriptor deployed',
    address: '0x01b44e7D89AF02dcda3E0985DAbaC636Dd0538D2',
    hash: '0xf2f8da3dff4cc141c7a380834a634bc459295fd6f3e7c333d2eebc908f8b7e38'
  }
]
Step 8 complete [
  {
    message: 'Contract TransparentUpgradeableProxy deployed',
    address: '0x339c373c1750C37F9019A13A372AA85cb708ff74',
    hash: '0xfdcb291c4411f86daaba5e1b7bc3b1058b9c74c4f3511698a6356af49898a895'
  }
]
Step 9 complete [
  {
    message: 'Contract NonfungiblePositionManager deployed',
    address: '0xC3a608a5012890F2A9B8F155fbd3E13608F69d18',
    hash: '0xf0446db6280ff54261acf7874d5878cdec1c2811b740d2090b96c05f2eacdd56'
  }
]
Step 10 complete [
  {
    message: 'Contract V3Migrator deployed',
    address: '0xC1198e6c907ad8Fadd0e7413562E343a5229807F',
    hash: '0x1271e764484df884758855f2929f19eeaa2abc92a0a60234877fba087d68cd32'
  }
]
Step 11 complete [
  {
    message: 'UniswapV3Factory owned by 0x0AF409EF995f90758470883AEfE220b3cAf853C6 already'
  }
]
Step 12 complete [
  {
    message: 'Contract UniswapV3Staker deployed',
    address: '0x4B380D0F8C9A47b79D3F2D4296C0b57222d9020F',
    hash: '0x1afbfae7b3593b6c6e620ff5261042b72420e7c418516dc8699fad88edcc38fb'
  }
]
Step 13 complete [
  {
    message: 'Contract QuoterV2 deployed',
    address: '0xD74331E1f9259aef7D6496409041b3edA9d2954c',
    hash: '0xba5caff8175993a2d24d73770556edb7830808c246e7535d75b54a5184f8262f'
  }
]
Step 14 complete [
  {
    message: 'Contract SwapRouter02 deployed',
    address: '0x940f7a59BCaCdb2561b3c4eD2BA04d760b3f0e64',
    hash: '0xbf6c00a4ce527c65a1f3ab82654c58489d93feb53c36b798acb6ed6e4ad94fef'
  }
]
Step 15 complete [
  {
    message: 'ProxyAdmin owned by 0x0AF409EF995f90758470883AEfE220b3cAf853C6 already'
  }
]
Deployment succeeded
[[{"message":"Contract UniswapV3Factory deployed","address":"0x7dEe2742F95516023Ea772e76eF42F15C94233F6","hash":"0xd0ea6ae81d854aebc6152f9c2e35eeaaf2b9823522bf33b31d0cab24f1410d63"}],[{"message":"UniswapV3Factory added a new fee tier 1 bps with tick spacing 1","hash":"0x66ee755b5c9cd96ac6029ad316dd0c829b3fce230ba5421a9e711c383df5e9b6"}],[{"message":"Contract UniswapInterfaceMulticall deployed","address":"0x3EEd5a7fAd89C3BA937f7Bc43d2097E7C351b8E3","hash":"0x881356a2a0f272593e055df7b9e06a5fe60573ff816753705013e48039d096f4"}],[{"message":"Contract ProxyAdmin deployed","address":"0x95CC6A7Ee69dB956692f8639b9B2FF5C20Cd046A","hash":"0xfc282ea62b3dca4a7debfb82df61aca3b8c1916a300a69101630e4194a790834"}],[{"message":"Contract TickLens deployed","address":"0x9DACFb107BC91F11234b62A82553f318cf0010b4","hash":"0x49dfad51c30469ff002e1ecf9abfa8deaa04a0da2159ea48ccb051754ee6fd77"}],[{"message":"Library NFTDescriptor deployed","address":"0x2A62BAf93A771dF1aA719edFdBE906F8271faa0E","hash":"0x5faead41ad23bcb59d298f8b86c232179e44d27a5bc01831a56a8f4c35cafccc"}],[{"message":"Contract NonfungibleTokenPositionDescriptor deployed","address":"0x01b44e7D89AF02dcda3E0985DAbaC636Dd0538D2","hash":"0xf2f8da3dff4cc141c7a380834a634bc459295fd6f3e7c333d2eebc908f8b7e38"}],[{"message":"Contract TransparentUpgradeableProxy deployed","address":"0x339c373c1750C37F9019A13A372AA85cb708ff74","hash":"0xfdcb291c4411f86daaba5e1b7bc3b1058b9c74c4f3511698a6356af49898a895"}],[{"message":"Contract NonfungiblePositionManager deployed","address":"0xC3a608a5012890F2A9B8F155fbd3E13608F69d18","hash":"0xf0446db6280ff54261acf7874d5878cdec1c2811b740d2090b96c05f2eacdd56"}],[{"message":"Contract V3Migrator deployed","address":"0xC1198e6c907ad8Fadd0e7413562E343a5229807F","hash":"0x1271e764484df884758855f2929f19eeaa2abc92a0a60234877fba087d68cd32"}],[{"message":"UniswapV3Factory owned by 0x0AF409EF995f90758470883AEfE220b3cAf853C6 already"}],[{"message":"Contract UniswapV3Staker deployed","address":"0x4B380D0F8C9A47b79D3F2D4296C0b57222d9020F","hash":"0x1afbfae7b3593b6c6e620ff5261042b72420e7c418516dc8699fad88edcc38fb"}],[{"message":"Contract QuoterV2 deployed","address":"0xD74331E1f9259aef7D6496409041b3edA9d2954c","hash":"0xba5caff8175993a2d24d73770556edb7830808c246e7535d75b54a5184f8262f"}],[{"message":"Contract SwapRouter02 deployed","address":"0x940f7a59BCaCdb2561b3c4eD2BA04d760b3f0e64","hash":"0xbf6c00a4ce527c65a1f3ab82654c58489d93feb53c36b798acb6ed6e4ad94fef"}],[{"message":"ProxyAdmin owned by 0x0AF409EF995f90758470883AEfE220b3cAf853C6 already"}]]
Final state
{"v3CoreFactoryAddress":"0x7dEe2742F95516023Ea772e76eF42F15C94233F6","multicall2Address":"0x3EEd5a7fAd89C3BA937f7Bc43d2097E7C351b8E3","proxyAdminAddress":"0x95CC6A7Ee69dB956692f8639b9B2FF5C20Cd046A","tickLensAddress":"0x9DACFb107BC91F11234b62A82553f318cf0010b4","nftDescriptorLibraryAddressV1_3_0":"0x2A62BAf93A771dF1aA719edFdBE906F8271faa0E","nonfungibleTokenPositionDescriptorAddressV1_3_0":"0x01b44e7D89AF02dcda3E0985DAbaC636Dd0538D2","descriptorProxyAddress":"0x339c373c1750C37F9019A13A372AA85cb708ff74","nonfungibleTokenPositionManagerAddress":"0xC3a608a5012890F2A9B8F155fbd3E13608F69d18","v3MigratorAddress":"0xC1198e6c907ad8Fadd0e7413562E343a5229807F","v3StakerAddress":"0x4B380D0F8C9A47b79D3F2D4296C0b57222d9020F","quoterV2Address":"0xD74331E1f9259aef7D6496409041b3edA9d2954c","swapRouter02":"0x940f7a59BCaCdb2561b3c4eD2BA04d760b3f0e64"}
```

## Usage

This package vends a CLI for executing a deployment script that results in a full deployment of Uniswap Protocol v3.
Get the arguments for running the latest version of the script via `npx @uniswap/deploy-v3 --help`.

As of `v1.0.3` the arguments are:

```text
> npx @uniswap/deploy-v3 --help
Usage: npx @uniswap/deploy-v3 [options]

Options:
  -pk, --private-key <string>               Private key used to deploy all contracts
  -j, --json-rpc <url>                      JSON RPC URL where the program should be deployed
  -w9, --weth9-address <address>            Address of the WETH9 contract on this chain
  -ncl, --native-currency-label <string>    Native currency label, e.g. ETH
  -o, --owner-address <address>             Contract address that will own the deployed artifacts after the script runs
  -s, --state <path>                        Path to the JSON file containing the migrations state (optional) (default: "./state.json")
  -v2, --v2-core-factory-address <address>  The V2 core factory address used in the swap router (optional)
  -g, --gas-price <number>                  The gas price to pay in GWEI for each transaction (optional)
  -c, --confirmations <number>              How many confirmations to wait for after each transaction (optional) (default: "2")
  -V, --version                             output the version number
  -h, --help                                display help for command
```

The script runs a set of migrations, each migration deploying a contract or executing a transaction. Migration state is
saved in a JSON file at the supplied path (by default `./state.json`).

To use the script, you must fund an address, and pass the private key of that address to the script so that it can construct
and broadcast the deployment transactions.

The block explorer verification process (e.g. Etherscan) is specific to the network. For the existing deployments,
we have used the `@nomiclabs/hardhat-etherscan` hardhat plugin in the individual repositories to verify the deployment addresses.

Note that in between deployment steps, the script waits for confirmations. By default, this is set to `2`. If the network
only mines blocks when the transactions is queued (e.g. a local testnet), you must set confirmations to `0`.

## Development

To run unit tests, run `yarn test`.

For testing the script, run `yarn start`.

To publish the script, first create a version: `npm version <version identifier>`, then publish via `npm publish`.
Don't forget to push your tagged commit!

## FAQs

### How much gas should I expect to use for full completion?

We estimate 30M - 40M gas needed to run the full deploy script.

### When I run the script, it says "Contract was already deployed..."

Delete `state.json` before a fresh deploy. `state.json` tracks which steps have already occurred. If there are any entries, the deploy script will attempt to pick up from the last step in `state.json`.

### Where can I see all the addresses where each contract is deployed?

Check out `state.json`. It'll show you the final deployed addresses.

### How long will the script take?

Depends on the confirmation times and gas parameter. The deploy script sends up to a total of 14 transactions.

### Where should I ask questions or report issues?

You can file them in `issues` on this repo and we'll try our best to respond.
