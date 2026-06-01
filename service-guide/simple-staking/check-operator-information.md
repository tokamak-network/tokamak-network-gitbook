---
description: >-
  Look up registered operators (DAO candidates), their staking totals, and L2
  sequencer details on Etherscan.
---

# Check operator information

Operators (DAO candidates) are registered in the **Layer2Registry** contract. From there you can reach each operator's Candidate contract, its operator manager, and — for L2 sequencers — its rollup and bridge details.

* Layer2Registry: [0x7846c2248a7b4de77e9c2bae7fbb93bfc286837b](https://etherscan.io/address/0x7846c2248a7b4de77e9c2bae7fbb93bfc286837b)
* Layer2Manager: [0xD6Bf6B2b7553c8064Ba763AD6989829060FdFC1D](https://etherscan.io/address/0xD6Bf6B2b7553c8064Ba763AD6989829060FdFC1D)
* SeigManager: [0x0b55a0f463b6defb81c6063973763951712d0e5f](https://etherscan.io/address/0x0b55a0f463b6defb81c6063973763951712d0e5f)
* WTON: [0xc4A11aaf6ea915Ed7Ac194161d2fC9384F15bff2](https://etherscan.io/address/0xc4A11aaf6ea915Ed7Ac194161d2fC9384F15bff2)

## Find an operator

### `numLayer2s()`

[Total number](https://etherscan.io/address/0x7846c2248a7b4de77e9c2bae7fbb93bfc286837b#readProxyContract) of registered Layer2 operators (networks).

* **Returns**: `uint256` — number of registered operators

### `layer2ByIndex(uint256 index)`

[Address of a registered operator](https://etherscan.io/address/0x7846c2248a7b4de77e9c2bae7fbb93bfc286837b#readProxyContract) by index.

* **Parameter**: `index` (starting at 0)
* **Returns**: `address` — the `candidateContract` at that index

<figure><img src="../../.gitbook/assets/staking-etherscan-operator-1.png" alt=""><figcaption><p>Open the returned address to reach the Candidate contract</p></figcaption></figure>

## Inspect a Candidate contract

Open the `candidateContract` address returned above, then use its **Read as Proxy** tab.

### `memo()`

The operator's name / memo. Use this to confirm you have the operator you want.

* **Returns**: `string` — operator name or memo

### `stakedOf(address user)`

Amount a specific user has staked to this operator.

* **Parameter**: `user` (address to query)
* **Returns**: `uint256` — amount staked by the user

### `totalStaked()`

Total amount staked to this operator.

* **Returns**: `uint256` — total staked to the operator

### `operator()`

The operator manager contract address.

* **Returns**: `address` — the operator manager contract (`operatorManager`)

<figure><img src="../../.gitbook/assets/staking-etherscan-operator-2.png" alt=""><figcaption><p>Check the operatorManager address</p></figcaption></figure>

## Inspect the operator manager (L2 sequencers)

Open the `operatorManager` address and use its **Read as Proxy** tab.

### `rollupConfig()`

The operator's RollupConfig contract address.

* **Returns**: `address` — RollupConfig contract address

<figure><img src="../../.gitbook/assets/staking-etherscan-operator-3.png" alt=""><figcaption><p>Check the rollupConfig address</p></figcaption></figure>

### `checkL1BridgeDetail(address rollupConfigAddress)` — on Layer2Manager

[Query L1 bridge details](https://etherscan.io/address/0xD6Bf6B2b7553c8064Ba763AD6989829060FdFC1D#readProxyContract) for a rollup.

* **Parameter**: `rollupConfigAddress` — the RollupConfig contract address
* **Returns**: `array` — L1 bridge details. If the value at index 5 is `1`, the operator is an L2 operator. If it is not an L2 operator, the queries below are not available.

### `optimismPortal()` — on the RollupConfig

The L2 bridge (Optimism Portal) address.

* **Returns**: `address` — L2 bridge address

## L2 sequencer seigniorage

The seigniorage an L2 sequencer can currently receive equals the WTON balance held by its operator manager **plus** the value returned by `estimatedDistribute`.

### `balanceOf(address account)` — on WTON

The WTON balance held by the operator manager contract.

* **Parameter**: `account` — the `operatorManager` address
* **Returns**: `uint256` — balance of the operator manager

### `estimatedDistribute(uint256 blockNumber, address opAddress)` — on SeigManager

[Expected seigniorage distribution](https://etherscan.io/address/0x0b55a0f463b6defb81c6063973763951712d0e5f#readProxyContract) for the next block.

* **Parameters**
  * `blockNumber`: current block number + 1
  * `opAddress`: the `candidateContract` address (from `layer2ByIndex`)
* **Returns**: `array` — distribution information; index 7 is the additional WTON to be distributed
