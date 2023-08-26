# Creating and Minting Token

This is a basic solidity smart contract for creating a customized token named "APACHE".

## Description

The given code is an example of a Solidity-written smart contract that generates a token named "APACHE" with the symbol "APC" on the Ethereum network. Let's examine its functions in detail:

Contract Inheritance: The contract is descended from the ERC20, ERC20Burnable, and Ownable contracts. These contracts, which are a part of the OpenZeppelin library, offer the ability to produce ERC20 tokens, allow token burning, and control ownership permissions.

Constructor: Upon contract deployment, the constructor function is called. By invoking the ERC20 contract's constructor with the parameters "APACHE" as the name and "APC" as the symbol, it initialises the token. It also creates 1 token, which is represented as 1 * 10 ** decimals(), and assigns it to the deployer's address (i.e., msg.sender).

The contract owner (deployer) may mint more tokens by using the mint function. It requires the two parameters amount and to, which provide the address and quantity of new tokens to be issued, respectively. The onlyOwner modifier, which is inherited from the Ownable contract, limits who can invoke the function to the contract owner only. Internally, the new coins are created and assigned to the designated address using the _mint function from the ERC20 contract.

This contract is for the creation of a token named "APACHE" with the symbol "APC" and an initial supply of one token. Additional tokens may be minted by the contract owner if needed.

## Getting Started

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., apache.sol). Copy and paste the following code into the file:

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MyToken is ERC20, Ownable {
    constructor() ERC20("APACHE", "APC") {}

    function mint(address account, uint256 amount) public onlyOwner {
        _mint(account, amount);
    }

    function burn(uint256 amount) public {
        _burn(msg.sender, amount);
    }

    function transfer(address recipient, uint256 amount) public override returns (bool) {
        require(recipient != address(0), "ERC20: transfer to the zero address is not allowed");
        return super.transfer(recipient, amount);
    }
}

```

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.9" (or another compatible version), and then click on the "Compile apache.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "apache" contract from the dropdown menu, and then click on the "Deploy" button.

To deploy on hardhat network, run the following commands:

```
npx hardhat compile
npx hardhat node
node scripts/deploy.js

```


## Authors

Aditya Raju

adrocxsmma@gmail.com


## License

This project is licensed under the MIT License - see the LICENSE.md file for details
