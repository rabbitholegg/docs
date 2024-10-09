Etherscan is a valuable tool for finding the right information to set up actions for your boost. This guide will help you navigate Etherscan to identify key elements needed for your boost action.

## Getting Started

1. Go to [Etherscan.io](https://etherscan.io/)
2. In the search bar at the top, paste a transaction hash
3. Press Enter or click the search icon

## Key Elements to Look For

### 1. Action Section

#### From
- **Where**: Look for "From:" near the top of the Etherscan page
- **What**: The address that sent the transaction
- **Usage**: Enter this in the "From" field of the Boost Deploy flow to target transactions from specific addresses

#### To
- **Where**: Look for "To:" just below "From:"
- **What**: The address of the contract being interacted with
- **Usage**: Enter this in the "To" field to target interactions with a specific contract

#### Value
- **Where**: Look for "Value:" in the transaction details
- **What**: The amount of ETH sent with the transaction
- **Usage**: Use this to set a value filter in the Boost Deploy flow

#### Signature
- **Where**: In the "Input Data" section
- **What**: The decoded function name (if contract is verified)
- **Usage**: Select this function in the "Signature" dropdown in the Boost Deploy flow

### 2. Parameter Filters

- **Where**: In the "Input Data" section, below the function name
- **What**: List of parameters and their values
- **Usage**: Set up parameter filters based on these values

### 3. Logs Section

#### Address
- **Where**: At the top of each log in the "Logs" section
- **What**: The contract address for the event
- **Usage**: Enter this in the "Address" field of the Log Filter

#### Signature
- **Where**: The event name in each log
- **What**: The name of the emitted event
- **Usage**: Select this event in the "Signature" dropdown of the Log Filter

#### Parameter Filters
- **Where**: Below the event name in each log
- **What**: List of parameters and their values for the event
- **Usage**: Set up parameter filters for log events

### 4. Claimant Information

- **Where**: Typically the same as the "From" address
- **What**: The address that performed the action you want to reward
- **Usage**: Use this address in the "Claimant" field of your boost configuration

## Tips for Effective Boost Setup

1. Start with the Contract ("To" field) to target a specific protocol or token
2. Use the "Signature" field to specify the exact function you're interested in
3. Utilize Parameter Filters to narrow down to significant actions
4. Leverage Log Filters to capture successful outcomes
5. Use the Claimant field to target specific user groups or exclude certain addresses

Remember to use the "Filter Preview" in the Boost Deploy flow to ensure your filters are capturing the intended transactions. Regularly review and refine your boost performance for optimal results.