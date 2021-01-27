BCDV 1010 : Lab - 3
=======================

1. Create a simple GBCToken contract that consists of -

   * map of balanceOf to store balances of the token
   * constructor to initialise the balance of contract creator with maximum number of token (total supply)
   * transfer function to transfer the token from the sender to someone.
        - It should be public so that everyone can use this function to send token to each other.
        - It should check whether the sender has enough tokens before transferring.
        - It should check for overflows before transferring.
        - It should emit a Transfer event

Test the contract on Remix, make sure constructor, balanceOf and transfer() are functional.



Solution
--------

.. code-block:: javascript
  :linenos:


  // SPDX-License-Identifier: MIT
  pragma solidity ^0.7.0;


  import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/math/SafeMath.sol";

  contract GBCToken {

      using SafeMath for uint;

      mapping (address => uint) balanceOf;

      event Transfer(address indexed _from,address indexed _to,uint indexed _amount);

      constructor(){
          balanceOf[msg.sender] = 5000;
      }

      function transfer(address _receiver, uint _amount) public returns(bool _sufficient){
          require(balanceOf[msg.sender] >= _amount, "Insufficient balance");
          balanceOf[msg.sender] = balanceOf[msg.sender] - _amount;
          balanceOf[_receiver] = balanceOf[_receiver] + _amount;
          emit Transfer(msg.sender, _receiver,_amount);
          _sufficient = true;
      }
  }

