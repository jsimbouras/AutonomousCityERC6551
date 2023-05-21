Simplified implementation of a DAO where each ERC6551 token holder has one vote.
Token holders can vote for proposals to create new ERC6551 accounts, and transfer ownership. 

Please note that this implementation assumes that you have already deployed the IERC6551Registry and IERC6551Account contracts separately. The registry variable is used to interact with the registry contract and create new ERC6551 accounts.
In this simplified DAO, each address that holds an ERC6551 token can vote once by calling the vote function. The createAccount function is used to create a new ERC6551 account and transfer the ownership of the token to that account.
The getVoteCount function allows querying the vote count of a specific address.
Make sure to replace the import statements with the correct paths to the IERC6551Registry and IERC6551Account contracts in your project.

Constructor:
The constructor takes two parameters: _registryAddress and _daoTokenContract. These parameters represent the addresses of the IERC6551Registry contract and the ERC6551 token contract, respectively.
The constructor initializes the registry variable with the IERC6551Registry contract instance and sets the daoTokenContract variable to the ERC6551 token contract address.
Vote:

The vote function allows token holders to cast their votes for a proposal.
It takes a proposalId parameter that represents the ID of the proposal being voted on.
Inside the function, it checks if the sender (voter) has already voted by verifying that their voteCount is 0. If the sender has already voted, it reverts with an error message.
If the sender hasn't voted, it sets their voteCount to 1 and emits a VoteCast event with the voter's address and the proposal ID.
CreateAccount:

The createAccount function is used to create a new ERC6551 account and transfer the ownership of the token to that account.
It takes four parameters: implementation, chainId, tokenContract, and tokenId.
Inside the function, it calls the createAccount function of the IERC6551Registry contract to create a new account based on the provided parameters.
Once the account is created, it uses the transferOwnership function of the IERC6551Account contract to transfer the ownership of the token to the newly created account.
getVoteCount:

The getVoteCount function allows querying the vote count of a specific address.
It takes an voter parameter representing the address for which we want to retrieve the vote count.
It returns the vote count associated with the given address.

pragma solidity ^0.8.0;

import "IERC6551Registry.sol";
import "IERC6551Account.sol";

contract SimpleDAO {
    IERC6551Registry private registry;
    address private daoTokenContract;
    
    mapping(address => uint256) private voteCount;
    
    event VoteCast(address indexed voter, uint256 proposalId);
    
    constructor(address _registryAddress, address _daoTokenContract) {
        registry = IERC6551Registry(_registryAddress);
        daoTokenContract = _daoTokenContract;
    }
    
    function vote(uint256 proposalId) external {
        address voter = msg.sender;
        require(voteCount[voter] == 0, "Already voted");
        voteCount[voter] = 1;
        emit VoteCast(voter, proposalId);
    }
    
    function createAccount(
        address implementation,
        uint256 chainId,
        address tokenContract,
        uint256 tokenId
    ) external {
        address accountAddress = registry.createAccount(implementation, chainId, tokenContract, tokenId);
        // Transfer the ERC6551 token ownership to the accountAddress
        IERC6551Account(accountAddress).transferOwnership(tokenContract, tokenId);
    }
    
    function getVoteCount(address voter) external view returns (uint256) {
        return voteCount[voter];
    }



}
