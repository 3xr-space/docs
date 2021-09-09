# Documents

House of relevant [3XR](https://3xr.space) documentation.


## Custom galleries

With efforts to make custom spaces a reality, [3XR.SPACE](https://3xr.space) now renders galleries as NFTs. How can you do this?

- Mint an NFT on Mintbase with custom key-value (extra tab on the minter)
- Add `asset_places`, `gallery_nfts`, `space_colors` and `external_space` to the extra field. Using the following types as an example:

```tsx

type AssetPlace = {
  position: Vector3,
  rotation: Euler
}

type Color = {
  [id: String]: string
}

type extra = {
  asset_places: AssetPlace[],
  gallery_nfts: string[], // each string is a Mintbase Thing Id (ex: 20uY0kXV-OgiCL6FGN5WFSb-e8BJ1Kn7nRACHF5r9cI:vrchallenge.mintspace2.testnet)
  space_colors: Color[],
  external_space: string // A URL to an off-chain React Remote Component
}

```

To learn more about React Remote Components check out: https://github.com/Paciolan/remote-component#what-is-a-remote-component?
3XR was modified today (September 9, 2021) to render Remote Components that are served from `external_space`.


All of this will be likely changed in the short term and was mostly modified to help a hacker [@sainthiago](https://github.com/sainthiago) during the MetaBUIDL hack to complete his challenge.


## Wallet Connection

3XR uses [Mintbase.js](https://github.com/Mintbase/mintbase-js) to connect uses to the [NEAR]() wallet.


## Environments: Testnet and Mainnet

3XR now works for both NEAR testnet and mainnet.

- Testnet: https://testnet.3xr.space
- Mainnet: https://mainnet.3xr.space or https://3xr.space
