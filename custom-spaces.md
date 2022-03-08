## [WIP] Custom Spaces (v2) - Initial Draft

Evolving from the [Custom Galleries](#v1) concept that was first released in October 2021, and launched in January 2022. 

The new standard aims to address the minting of an NFT as a space composed of information related to NFTs from other ecosystems. 

### Space NFT

In our first iteration, we adopted the [Attributes](https://docs.opensea.io/docs/metadata-standards#attributes) metadata standard for the `extra` field. This remains true for v2 but we're renaming a few properties and adding some extra ones such as:

```ts

type StandardVersion = string // (ex. "2.0.0")

type Vector3 = {
  x: number
  y: number
  z: number
}

type Euler = {
  x: number
  y: number
  z: number
  order: string // (ex. "XYZ")
}

type Scale = {
  x: number
  y: number
  z: number
}

type FilePreference = {
  MediaType: string // (ex. "model/gltf-binary", see: https://www.iana.org/assignments/media-types/media-types.xhtml)
}

type AssetConfiguration = {
  position: Vector3
  rotation: Euler
  scale: Scale
}

type Reference = {
  id: string
  address: string
  chain: string 
  network: string  

  reference: string
  reference_hash: string
  file: string
  file_hash: string
}

type Asset = {
  place: AssetConfiguration
  reference: Reference[]
}

type Colors = {
  [id: string]: string
}

type SpaceWrapper = {
  place: AssetConfiguration
  reference: Reference[]
}

type Space = {
  standard_version: StandardVersion
  assets: Asset[]
  colors: Colors
  space_wrapper: SpaceWrapper
}

```

### Resolving NFT Spaces

The resolver will first check the version of the NFT and will use the best resolver. In the absence of the `standard_version` the resolver will default to v1.

### Challenges
- [ ] Resolve Reference to metadata


<a id="v1"></a>
## Custom Galleries (v1)

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

### How to generate a React component from a glTF file?

Use https://gltf.pmnd.rs/
