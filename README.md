# Ex_No_2_Blockchain-Based-Crowdfunding-Kickstarter-Alternative-

# AIM:
To create a decentralized crowdfunding platform where donors contribute funds only if the campaign goal is met.

# Alogrithm:

1.A project owner starts a campaign with a funding goal and deadline.

2.Contributors can send ETH to the campaign.

3.If the goal is met before the deadline, funds are released to the project owner.

4.If the goal is not met, contributors can withdraw their funds.

# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Crowdfunding {
    struct Campaign {
        address creator;
        uint256 goal;
        uint256 deadline;
        uint256 amountRaised;
        bool goalMet;
        mapping(address => uint256) contributions;
    }

    Campaign public campaign;

    constructor(uint256 _goal, uint256 _duration) {
        campaign.creator = msg.sender;
        campaign.goal = _goal;
        campaign.deadline = block.timestamp + _duration;
    }

    function contribute() public payable {
        require(block.timestamp < campaign.deadline, "Campaign ended");
        campaign.amountRaised += msg.value;
        campaign.contributions[msg.sender] += msg.value;
    }

    function withdrawFunds() public {
        require(msg.sender == campaign.creator, "Only creator can withdraw");
        require(campaign.amountRaised >= campaign.goal, "Goal not met");
        payable(msg.sender).transfer(campaign.amountRaised);
        campaign.goalMet = true;
    }

    function refund() public {
        require(block.timestamp > campaign.deadline, "Campaign still active");
        require(campaign.amountRaised < campaign.goal, "Goal was met");
        uint256 amount = campaign.contributions[msg.sender];
        campaign.contributions[msg.sender] = 0;
        payable(msg.sender).transfer(amount);
    }
}
```

# Expected output
<img width="1427" height="486" alt="image" src="https://github.com/user-attachments/assets/0a9939bd-6ea9-4243-9275-9bf5cc4356eb" />

# High Overview
<img width="1422" height="722" alt="image" src="https://github.com/user-attachments/assets/6fccf7d0-d217-4b33-8732-32afd6e58616" />


# Result
Thus the crowdfunding by the contributor met the campagin.
