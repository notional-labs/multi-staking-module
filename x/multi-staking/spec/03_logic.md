

## BondDenom Selection Logic

* `BondDenom` and `BondTokenWeight` are the multi-staking module's parameters.
* When setting new parameters, the module will validate whether the address sending the message is authority address.
* The authority address is the government module's address.
* Therefore, changes to the bond denom token list and bond denom token weight will only occur through a governance proposal.

## Validator Creation

* Coins sent through `MsgCreateValidator` must be included in the `BondDenom` token list.
* Based on the `BondTokenWeight` parameter, an amount of `stake` will be minted:`mintAmount = BondTokenWeight * msg.Value.Amount`.
* The multi-staking module will then call the staking module to create a validator with the minted `stake` tokens as delegation.
* Finally, the multi-staking module will save validator information regarding the bond denom token, and this validator denom will be immutable: `ValOperatorAddr -> BondDenom`.