// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Bank {
    // Mapping to store balances of each account
    mapping(address => uint256) private balances;

    // Function to deposit money into the bank
    function deposit() public payable {
        require(msg.value > 0, "Deposit amount must be greater than 0");
        balances[msg.sender] += msg.value;
    }

    // Function to withdraw money from the bank
    function withdraw(uint256 amount) public {
        require(balances[msg.sender] >= amount, "Insufficient balance");
        balances[msg.sender] -= amount;
        payable(msg.sender).transfer(amount);
    }

    // Function to check the balance of the account
    function getBalance() public view returns (uint256) {
        return balances[msg.sender];
    }
}
