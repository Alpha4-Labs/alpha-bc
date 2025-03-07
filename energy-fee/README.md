# Energy Fee Pallet

The **Energy Fee Pallet** implements a dual-token transaction fee mechanism that allows transactions to be paid using both the native token and energy tokens (VNRG). It dynamically adjusts fees based on network conditions to ensure efficient and fair resource usage.

## Features

- **Dual-token fee system**: Supports payment in both native tokens and VNRG.
- **Dynamic fee adjustments**: Adapts based on block fullness and network congestion.
- **Token exchange mechanism**: Allows automatic swapping of native tokens for energy.
- **EVM transaction fee handling**: Supports Ethereum-compatible transaction fees.
- **Energy burning threshold**: Helps prevent spam and abuse.

## Fee Calculation

Fees are determined based on the following factors:

- **Base fee**: A fixed minimum fee applied to all transactions.
- **Dynamic multiplier**: Adjusted based on block fullness to manage congestion.
- **Custom fee logic**: Allows defining specific fees for different extrinsics.
- **EVM fees**: Specialized handling for Ethereum-compatible transactions.

## Security Considerations

- **Spam protection**: The fee-burning mechanism prevents network spam and denial-of-service (DoS) attacks.
- **Congestion control**: Fee multipliers prevent excessive network congestion.
- **Exchange security**: The automatic token exchange system prevents manipulation.
- **Authorized control**: Only privileged accounts can modify system parameters.

## Configuration

The pallet requires the following configuration parameters:

- `ManageOrigin`: Defines the authority that can modify fee parameters.
- `GetConstantFee`: Specifies the base fee amount.
- `CustomFee`: Implements custom fee logic for different extrinsics.
- `EnergyAsset`: Handles operations related to VNRG tokens.
- `EnergyExchange`: Manages the exchange of native tokens for energy.

## Storage

The pallet maintains the following storage values:

- `BurnedEnergy`: Tracks the total amount of burned energy.
- `BurnedEnergyThreshold`: Defines the limit at which fee burning stops.
- `BlockFullnessThreshold`: Determines when fee multipliers are adjusted.
- `UpperFeeMultiplier`: Sets the upper limit for fee adjustments.
- `BaseFee`: Stores the base transaction fee.

## Events

The following events are emitted by the pallet:

- `EnergyFeePaid`: Emitted when an energy fee is paid.
- `BurnedEnergyThresholdUpdated`: Triggered when the energy burning threshold changes.
- `BlockFullnessThresholdUpdated`: Triggered when the block fullness threshold is modified.
- `UpperFeeMultiplierUpdated`: Emitted when the upper fee multiplier is updated.

## Extrinsics

The pallet provides the following extrinsics:

- `update_burned_energy_threshold(new_threshold)`: Updates the energy-burning threshold.
- `update_block_fullness_threshold(new_threshold)`: Adjusts the block fullness threshold.
- `update_upper_fee_multiplier(new_multiplier)`: Modifies the upper fee multiplier.
- `update_base_fee(new_base_fee)`: Sets a new base transaction fee.

## Implementation Details

This pallet integrates with the `pallet-evm` and `pallet-transaction-payment` to handle both standard Substrate transactions and Ethereum-compatible transactions. The `OnChargeTransaction` and `OnChargeEVMTransaction` traits are implemented to facilitate the fee deduction process.

## License

This project is licensed under the Apache 2.0 License.
