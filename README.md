ETH-AVAX-Final-Project
This is a project intended for a submission to the ETH-AVAX final assesment and fulfills all the requirements that it has, 
The project does the following: 
- Minting new tokens: The platform should be able to create new tokens and distribute them to players as rewards. Only the owner can mint tokens.
- Transferring tokens: Players should be able to transfer their tokens to others.
- Redeeming tokens: Players should be able to redeem their tokens for items in the in-game store.
- Checking token balance: Players should be able to check their token balance at any time.
- Burning tokens: Anyone should be able to burn tokens, that they own, that are no longer needed.


## Getting Started
Go to snowtrace.io and enter the following in the Searchbar 
"0x84f2BdFF2BB675702B3050422CF3Fbb866c30e4D" 
This shows up the particular instance of the token that we have minted onto the block chain. 

### Executing program
o run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. 
Save the file with a .sol extension. Copy and paste the following code into the file:

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract DegenToken is ERC20, Ownable {

     constructor() ERC20("Degen", "DGN") Ownable(msg.sender) {}

    // Events
    event TokensRedeemed(address indexed from, uint256 amount);
    event TokensBurned(address indexed from, uint256 amount);


    // Function to allow the owner to mint new tokens and distribute them as rewards.
    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }

    // Function to allow players to transfer tokens to others.
    function transfer(address to, uint256 amount) public override returns (bool) {
        return super.transfer(to, amount);
    }

    // Function to allow players to redeem tokens for items in the in-game store.
    function redeem(uint256 amount) public returns (bool) {
        require(balanceOf(msg.sender) >= amount, "Not enough tokens");
        _burn(msg.sender, amount);

        // Emit event
        emit TokensRedeemed(msg.sender, amount);
        return true;
    }

    // Function to check the token balance of a player.
    function checkBalance(address account) public view returns (uint256) {
        return balanceOf(account);
    }

    // Function to allow anyone to burn their own tokens that are no longer needed.
    function burn(uint256 amount) public {
        require(balanceOf(msg.sender) >= amount, "Not enough tokens to burn");
        
        // Burn the tokens
        _burn(msg.sender, amount);

        // Emit event
        emit TokensBurned(msg.sender, amount);
    }
}
```

##Afterwards
To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.18" (or another compatible version), and then click on the "Compile reqasrev.sol" button. 

The button name can vary depending on the file name that you designated when creating the file of the code.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the contract with the same name of the file you have just compiled (e.g if your file has the name "HelloWorld.sol" the option to click should be "HelloWorld") from the dropdown menu. 

To continue on first we have to change the environment to "Injected Provider". 

Afterwards we connect the page to our Metamask account and we should take note of the account number here. 

We then go back to the snowtrace and copy the Contract Address where in this case should be "0x84f2BdFF2BB675702B3050422CF3Fbb866c30e4D". 
We paste this into the the blue button that says "At Address" and copy that address to the textbox next to it and press it instead of the usual Deploy button.

To interact with the code it is fairly simple: 
- with burn we simply have to indicate the amount of coins to be burnt as long as the balance is sufficient
- With mint we give the account number to minted to and the amount
- with redeem we indicate the amount of coins that will be used to redeem a certain item
- transfer will transfer coins as long as you indicate the address to transfer to and the amount
- and finally balanceOf or CheckBalance both do the same of checking the current balance of the address account indicated.


Once the contract is deployed, you can interact with it by calling the mint, burn, redeem, transfer, and balanceOf functions. 


## Authors

Contributors names and contact info
Gavinno Othello C. Angeles

email me at: 201911104@fit.edu.ph

## License

This project is licensed under the MIT License - see the LICENSE.md file for details
