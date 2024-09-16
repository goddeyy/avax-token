# Goddey Coin (GDC) Token Contract

## Description

This Solidity program outlines the `GoddeyCoin` contract, an ERC-20 token with the symbol `GDC`. It serves as an introduction to token creation on the Ethereum blockchain, incorporating the fundamental features of the ERC-20 standard. The contract includes additional functionalities for minting, burning, and transferring tokens, which extend the basic ERC-20 implementation. This contract is ideal for those looking to understand token management and smart contract deployment.

## Getting Started

### Executing the Program

To run this contract, you can use Remix, an online Solidity IDE. Follow these steps to get started:

1. **Open Remix:**
   Go to the Remix IDE website at [https://remix.ethereum.org/](https://remix.ethereum.org/).

2. **Create a New File:**
   Click on the "+" icon in the left-hand sidebar to create a new file. Save it with a `.sol` extension (e.g., `GoddeyCoin.sol`).

3. **Add the Contract Code:**
   Copy and paste the following code into the newly created file:

   ```solidity
   // SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract GoddeyCoin is ERC20 {
    address public owner;

    modifier onlyOwner() {
        require(msg.sender == owner, "Only owner can mint");
        _;
    }

    constructor() ERC20("GoddeyCoin", "GDC") {
        owner = msg.sender;
    }

    function mint(address _to, uint256 _amount) public onlyOwner {
        _mint(_to, _amount * (10 ** decimals()));
    }

    function transfer(address to, uint256 value) public virtual override returns (bool success) {
        require(balanceOf(msg.sender) >= value, "Insufficient balance");
        success = super.transfer(to, value);
    }

    function burn(uint256 _amount) public {
        require(balanceOf(msg.sender) >= _amount, "Insufficient balance");
        _burn(msg.sender, _amount);
    }
}
   ```

4. **Compile the Code:**
   Click on the "Solidity Compiler" tab in the left-hand sidebar. Ensure the "Compiler" option is set to "0.8.13" (or a compatible version), and then click on the "Compile GoddeyCoin.sol" button.

5. **Deploy the Contract:**
   Navigate to the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the `GoddeyCoin` contract from the dropdown menu, and then click on the "Deploy" button.

6. **Interact with the Contract:**
   After deployment, you can interact with the contract through the "GoddeyCoin" section in the left-hand sidebar. Use the `mint` function to create new tokens (restricted to the owner) and the `burn` function to destroy tokens from your balance.

## License

This project is licensed under the MIT License
