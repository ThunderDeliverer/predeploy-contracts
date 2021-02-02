# Predeploy-contracts

Generate bytecode for predeployment of ERC20 smart contracts in Acala.

## Build

Run `yarn` to install dependencies.

## Generate bytecode

To generate bytecode, run `yarn run generate-bytecode`.

The generated bytecode JSON file would be `./resources/bytecodes.json`. The contracts are in `./contracts/tmp/` directory.

## Development

The token list for ERC20 smart contracts is in `./resources/tokens.json`. Name, symbol and Currency ID bytes are needed for each token, for instance:

```
{
  "name": "ACA",
  "symbol": "ACA",
  "currencyId": "0x0000"
}
```


# Predeployed System Contracts

## ERC20 Contracts
These ERC20 contracts make native and cross-chain tokens available inside Acala EVM.
- ACA contract address: `0x0000000000000000000000000000000000000800`.
- AUSD contract address: `0x0000000000000000000000000000000000000801`.
- DOT contract address: `0x0000000000000000000000000000000000000802`.
- XBTC contract address: `0x0000000000000000000000000000000000000803`.
- LDOT contract address: `0x0000000000000000000000000000000000000804`.
- RENBTC contract address: `0x0000000000000000000000000000000000000805`.
```
// Returns the currencyId of the token.
function currencyId() public view returns (uint256);

// Returns the name of the token.
function name() public view returns (string memory);

// Returns the symbol of the token, usually a shorter version of the name.
function symbol() public view returns (string memory);

// Returns the number of decimals used to get its user representation.
function decimals() public view returns (uint8);

// Returns the amount of tokens in existence.
function totalSupply() public view returns (uint256);

// Returns the amount of tokens owned by `account`.
function balanceOf(address account) public view returns (uint256);

// Moves `amount` tokens from the caller's account to `recipient`.
// Returns a boolean value indicating whether the operation succeeded.
// Emits a {Transfer} event.
function transfer(address recipient, uint256 amount) public returns (bool);

// Returns the remaining number of tokens that `spender` will be allowed to spend on behalf of `owner` through {transferFrom}. 
// This is zero by default.
function allowance(address owner, address spender) public view returns (uint256);

// Sets `amount` as the allowance of `spender` over the caller's tokens.
// Returns a boolean value indicating whether the operation succeeded.
function approve(address spender, uint256 amount) public returns (bool);

// Moves `amount` tokens from `sender` to `recipient` using the allowance mechanism. `amount` is then deducted from the caller's allowance.
// Returns a boolean value indicating whether the operation succeeded.
function transferFrom(address sender, address recipient, uint256 amount) public returns (bool);

// Atomically increases the allowance granted to `spender` by the caller.
// This is an alternative to {approve} that can be used as a mitigation for problems described in {IERC20-approve}.
// Emits an {Approval} event indicating the updated allowance.
function increaseAllowance(address spender, uint256 addedValue) public returns (bool);

// Atomically decreases the allowance granted to `spender` by the caller.
// This is an alternative to {approve} that can be used as a mitigation for problems described in {IERC20-approve}.
// Emits an {Approval} event indicating the updated allowance.
function decreaseAllowance(address spender, uint256 subtractedValue) public returns (bool);
```


## Other System Contracts:
These contracts make other chain-native functionalities available in Acala EVM.

### Oracle Price Feed
- Oracle contract address: `0x0000000000000000000000000000000000000807`
```
// Get the price of the currency_id.
// Returns the (price, timestamp)
function getPrice(address token) public view returns (uint256, uint256);
```
### On-chain Automatic Scheduler
- ScheduleCall contract address: `0x0000000000000000000000000000000000000808`
```
// Schedule call the contract.
// Returns the task_address(block_number, index).
function scheduleCall(address contract_address, uint256 value, uint256 gas_limit, uint256 storage_limit, uint256 min_delay, bytes memory input_data) public returns (uint256, uint256);
```
### State Rent
- StateRent contract address: `0x0000000000000000000000000000000000000806`
```
// Returns the const of NewContractExtraBytes.
function newContractExtraBytes() public view returns (uint256);

// Returns the const of StorageDepositPerByte.
function storageDepositPerByte() public view returns (uint256);

// Returns the maintainer of the contract.
function maintainerOf(address contract_address) public view returns (address);

// Returns the const of DeveloperDeposit.
function developerDeposit() public view returns (uint256);

// Returns the const of DeploymentFee.
function deploymentFee() public view returns (uint256);

// Transfer the maintainer of the contract.
// Returns a boolean value indicating whether the operation succeeded.
function transferMaintainer(address contract_address, address new_maintainer) public returns (bool);
```
## DeFi Contracts (Coming Soon)
These contracts will make Acala's DeFi primitives (stablecoin, staking derivative, and DeX) available in Acala EVM.

