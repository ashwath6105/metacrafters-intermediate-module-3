# Creating and Minting Token

This is a basic solidity smart contract for creating a customized token named "APACHE".

## Description

The provided Solidity smart contract, named MyToken, is an implementation of an ERC20 token with some additional functionalities. 

Name and Symbol: The contract inherits from the OpenZeppelin ERC20 contract, which is a widely used standard for fungible tokens on the Ethereum blockchain. The constructor initializes the token with the name "APACHE" and the symbol "APC".

Access Control: The contract also inherits from the Ownable contract, which provides basic access control functionality. This means that certain functions can only be executed by the contract owner.

Minting: The mint function allows the contract owner to create and assign new tokens to a specified address. This function can be used to increase the token supply. Only the contract owner can call this function due to the onlyOwner modifier.

Burning: The burn function enables any token holder to burn (destroy) a specified amount of their own tokens. This action permanently removes the burned tokens from circulation.

Transferring: The transfer function is an override of the ERC20 contract's standard transfer function. It allows users to transfer tokens from their own account to another account. The override adds a requirement that the recipient's address cannot be the zero address (address(0)), ensuring that tokens are not sent to a non-existent address.


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

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.0" (or another compatible version), and then click on the "Compile apache.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "apache" contract from the dropdown menu, and then click on the "Deploy" button.

To deploy on hardhat network, run the following commands:

```
npx hardhat compile
npx hardhat node
node scripts/deploy.js

```


## Authors

Ashwath R

ashwathraju85@gmail.com


## License

This project is licensed under the MIT License - see the LICENSE.md file for details
