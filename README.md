
# WOOFi Swap contest details

- Join [Sherlock Discord](https://discord.gg/MABEWyASkp)
- Submit findings using the issue page in your private contest repo (label issues as med or high)
- [Read for more details](https://docs.sherlock.xyz/audits/watsons)

# Q&A

### Q: On what chains are the smart contracts going to be deployed?
Mainnet (router, and crossswaprouter only)
All four contracts - Arbitrum, Optimism, Base, Avalanche, BSC, Polygon PoS, Mantle, Fantom, Polygon zkEVM, zkSync, Linea
___

### Q: Which ERC20 tokens do you expect will interact with the smart contracts? 
any
___

### Q: Which ERC721 tokens do you expect will interact with the smart contracts? 
none
___

### Q: Do you plan to support ERC1155?
none
___

### Q: Which ERC777 tokens do you expect will interact with the smart contracts? 
none
___

### Q: Are there any FEE-ON-TRANSFER tokens interacting with the smart contracts?

no
___

### Q: Are there any REBASING tokens interacting with the smart contracts?

no
___

### Q: Are the admins of the protocols your contracts integrate with (if any) TRUSTED or RESTRICTED?
Trusted
___

### Q: Is the admin/owner of the protocol/contracts TRUSTED or RESTRICTED?
Trusted
___

### Q: Are there any additional protocol roles? If yes, please explain in detail:
== WooPPV2.sol ==
  - "Owner" role: smart contract creator, multi-sig wallet, acess fund related actions ( rescue funds - inCaseTokenGotStuck, receive the funds withdrawn from wooPP pool, set lendingManager), plus all admin actions
  - "Admin" role: admin of contracts, admin actions: claimFee, setWooracle, setFeeAddr, setFeeRate, setMaxGamma, setMaxNotionalSwap, setTokenInfo, pause, unpause, deposit fund, repay lending, withdraw funds to contract owner, skim and sync pool balance
  - "PausableRole" role: only trigger "pause" function.

== WooracleV2_2.sol ==
  - "Owner" role: setAdmin, setBound and other onlyAdmin actions
  - "Admin" role: setWooPP, setQuoteToken, setCLOracle, setCloPreferred, setStaleDuration, postPrice/List, postState/List, syncTS, setBase, fallback, rescue funds to owner (inCaseTokenGotStuck)

== WooRouterV2.sol ==
  - "Owner" role: rescue fund (inCaseTokenGotStuck), setPool, setWhitelisted

== WooCrossChainRouterV4.sol ==
  - "Owner": setFeeAddr, setWooRouter, setBridgeSlippage, setWooCrossRouter, pause/unpause, rescue funds to owner - inCaseTokenGotStuck.

___

### Q: Is the code/contract expected to comply with any EIPs? Are there specific assumptions around adhering to those EIPs that Watsons should be aware of?
NO explicit EIP needed to comply.
___

### Q: Please list any known issues/acceptable risks that should not result in a valid finding.
n/a
___

### Q: Please provide links to previous audits (if any).
https://learn.woo.org/v/woofi-dev-docs/references/audits-and-bounties

___

### Q: Are there any off-chain mechanisms or off-chain procedures for the protocol (keeper bots, input validation expectations, etc)?
WOOFi's market maker uses offchain logic to update "Wooracle" contract's info (Threeparams: p - price, k - coefficient, s - spread).  These Wooracle parameters are utilized by SPMM formula to simulate the liquidity of CEX orderbook
___

### Q: In case of external protocol integrations, are the risks of external contracts pausing or executing an emergency withdrawal acceptable? If not, Watsons will submit issues related to these situations that can harm your protocol's functionality.
NO, we don't allow any external smart contracts to execute pause or emergency withdrawal, or other risky/abnormal actions.
___

### Q: Do you expect to use any of the following tokens with non-standard behaviour with the smart contracts?
NO.
___

### Q: Add links to relevant protocol resources
https://learn.woo.org/

The contract Woopp was exploited last week, where the exploiter took advantage of the sPMM formula and pushed WOO token price to almost zero. pls see details below
https://twitter.com/_WOOFi/status/1765150687166415129
___



# Audit scope


[WooPoolV2 @ f7886e8e362771fe00099872cca310e8558173dd](https://github.com/woonetwork/WooPoolV2/tree/f7886e8e362771fe00099872cca310e8558173dd)
- [WooPoolV2/contracts/CrossChain/WooCrossChainRouterV4.sol](WooPoolV2/contracts/CrossChain/WooCrossChainRouterV4.sol)
- [WooPoolV2/contracts/CrossChain/WooCrossRouterForWidget.sol](WooPoolV2/contracts/CrossChain/WooCrossRouterForWidget.sol)
- [WooPoolV2/contracts/WooPPV2.sol](WooPoolV2/contracts/WooPPV2.sol)
- [WooPoolV2/contracts/WooRouterV2.sol](WooPoolV2/contracts/WooRouterV2.sol)
- [WooPoolV2/contracts/wooracle/WooracleV2_2.sol](WooPoolV2/contracts/wooracle/WooracleV2_2.sol)

