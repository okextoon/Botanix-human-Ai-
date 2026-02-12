// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;
bitanix mainnet
import "@openzeppelin/contracts/access/Ownable.sol";

contract HumanAIAgent is Ownable {
    string public agentName;
    string public systemPromptHash; // IPFS hash of the AI's "personality"
    
    event ActionExecuted(string actionType, uint256 timestamp);

    constructor(string memory _name, string memory _promptHash) Ownable(msg.sender) {
        agentName = _name;
        systemPromptHash = _promptHash;
    }

    // AI can receive BTC (as synthetic BTC on Botanix)
    receive() external payable {}

    // Function for the AI controller to log actions
    uint256 public totalActions;
    function logAction(string memory actionType) public onlyOwner {
        totalActions++;
        emit ActionExecuted(actionType, block.timestamp);
    }

    function withdraw(uint256 amount) public onlyOwner {
        payable(owner()).transfer(amount);
    }
}
