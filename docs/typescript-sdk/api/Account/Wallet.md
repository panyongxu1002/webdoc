# Class: Wallet

[@fuel-ts/account](/api/Account/index).Wallet

`Wallet` provides methods to create locked and unlocked wallet instances.

## Constructors

### constructor

• **new Wallet**(): [`Wallet`](/api/Account/Wallet)

#### Returns

[`Wallet`](/api/Account/Wallet)

## Properties

### fromEncryptedJson

▪ `Static` **fromEncryptedJson**: (`jsonWallet`: `string`, `password`: `string`, `provider?`: [`Provider`](/api/Account/Provider)) => `Promise`&lt;[`WalletUnlocked`](/api/Account/WalletUnlocked)\> = `WalletUnlocked.fromEncryptedJson`

#### Type declaration

▸ (`jsonWallet`, `password`, `provider?`): `Promise`&lt;[`WalletUnlocked`](/api/Account/WalletUnlocked)\>

Create a Wallet Unlocked from an encrypted JSON.

##### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `jsonWallet` | `string` | The encrypted JSON keystore. |
| `password` | `string` | The password to decrypt the JSON. |
| `provider?` | [`Provider`](/api/Account/Provider) | A Provider instance (optional). |

##### Returns

`Promise`&lt;[`WalletUnlocked`](/api/Account/WalletUnlocked)\>

An unlocked wallet instance.

#### Defined in

[packages/account/src/wallet/wallet.ts:79](https://github.com/FuelLabs/fuels-ts/blob/6c4998c2/packages/account/src/wallet/wallet.ts#L79)

___

### fromExtendedKey

▪ `Static` **fromExtendedKey**: (`extendedKey`: `string`, `provider?`: [`Provider`](/api/Account/Provider)) => [`WalletUnlocked`](/api/Account/WalletUnlocked) = `WalletUnlocked.fromExtendedKey`

#### Type declaration

▸ (`extendedKey`, `provider?`): [`WalletUnlocked`](/api/Account/WalletUnlocked)

Create a Wallet Unlocked from an extended key.

##### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `extendedKey` | `string` | The extended key. |
| `provider?` | [`Provider`](/api/Account/Provider) | A Provider instance (optional). |

##### Returns

[`WalletUnlocked`](/api/Account/WalletUnlocked)

An unlocked wallet instance.

#### Defined in

[packages/account/src/wallet/wallet.ts:69](https://github.com/FuelLabs/fuels-ts/blob/6c4998c2/packages/account/src/wallet/wallet.ts#L69)

___

### fromMnemonic

▪ `Static` **fromMnemonic**: (`mnemonic`: `string`, `path?`: `string`, `passphrase?`: [`BytesLike`](/api/Interfaces/index.md#byteslike), `provider?`: [`Provider`](/api/Account/Provider)) => [`WalletUnlocked`](/api/Account/WalletUnlocked) = `WalletUnlocked.fromMnemonic`

#### Type declaration

▸ (`mnemonic`, `path?`, `passphrase?`, `provider?`): [`WalletUnlocked`](/api/Account/WalletUnlocked)

Create a Wallet Unlocked from a mnemonic phrase.

##### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `mnemonic` | `string` | The mnemonic phrase. |
| `path?` | `string` | The derivation path (optional). |
| `passphrase?` | [`BytesLike`](/api/Interfaces/index.md#byteslike) | The passphrase for the mnemonic (optional). |
| `provider?` | [`Provider`](/api/Account/Provider) | A Provider instance (optional). |

##### Returns

[`WalletUnlocked`](/api/Account/WalletUnlocked)

An unlocked wallet instance.

#### Defined in

[packages/account/src/wallet/wallet.ts:60](https://github.com/FuelLabs/fuels-ts/blob/6c4998c2/packages/account/src/wallet/wallet.ts#L60)

___

### fromSeed

▪ `Static` **fromSeed**: (`seed`: `string`, `path?`: `string`, `provider?`: [`Provider`](/api/Account/Provider)) => [`WalletUnlocked`](/api/Account/WalletUnlocked) = `WalletUnlocked.fromSeed`

#### Type declaration

▸ (`seed`, `path?`, `provider?`): [`WalletUnlocked`](/api/Account/WalletUnlocked)

Create a Wallet Unlocked from a seed.

##### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `seed` | `string` | The seed phrase. |
| `path?` | `string` | The derivation path (optional). |
| `provider?` | [`Provider`](/api/Account/Provider) | A Provider instance (optional). |

##### Returns

[`WalletUnlocked`](/api/Account/WalletUnlocked)

An unlocked wallet instance.

#### Defined in

[packages/account/src/wallet/wallet.ts:49](https://github.com/FuelLabs/fuels-ts/blob/6c4998c2/packages/account/src/wallet/wallet.ts#L49)

___

### generate

▪ `Static` **generate**: (`generateOptions?`: [`GenerateOptions`](/api/Account/GenerateOptions)) => [`WalletUnlocked`](/api/Account/WalletUnlocked) = `WalletUnlocked.generate`

#### Type declaration

▸ (`generateOptions?`): [`WalletUnlocked`](/api/Account/WalletUnlocked)

Generate a new Wallet Unlocked with a random key pair.

##### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `generateOptions?` | [`GenerateOptions`](/api/Account/GenerateOptions) | Options to customize the generation process (optional). |

##### Returns

[`WalletUnlocked`](/api/Account/WalletUnlocked)

An unlocked wallet instance.

#### Defined in

[packages/account/src/wallet/wallet.ts:39](https://github.com/FuelLabs/fuels-ts/blob/6c4998c2/packages/account/src/wallet/wallet.ts#L39)

## Methods

### fromAddress

▸ **fromAddress**(`address`, `provider?`): [`WalletLocked`](/api/Account/WalletLocked)

Creates a locked wallet instance from an address and a provider.

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `address` | `string` \| [`AbstractAddress`](/api/Interfaces/AbstractAddress) | The address of the wallet. |
| `provider?` | [`Provider`](/api/Account/Provider) | A Provider instance (optional). |

#### Returns

[`WalletLocked`](/api/Account/WalletLocked)

A locked wallet instance.

#### Defined in

[packages/account/src/wallet/wallet.ts:18](https://github.com/FuelLabs/fuels-ts/blob/6c4998c2/packages/account/src/wallet/wallet.ts#L18)

___

### fromPrivateKey

▸ **fromPrivateKey**(`privateKey`, `provider?`): [`WalletUnlocked`](/api/Account/WalletUnlocked)

Creates an unlocked wallet instance from a private key and a provider.

#### Parameters

| Name | Type | Description |
| :------ | :------ | :------ |
| `privateKey` | [`BytesLike`](/api/Interfaces/index.md#byteslike) | The private key of the wallet. |
| `provider?` | [`Provider`](/api/Account/Provider) | A Provider instance (optional). |

#### Returns

[`WalletUnlocked`](/api/Account/WalletUnlocked)

An unlocked wallet instance.

#### Defined in

[packages/account/src/wallet/wallet.ts:29](https://github.com/FuelLabs/fuels-ts/blob/6c4998c2/packages/account/src/wallet/wallet.ts#L29)
