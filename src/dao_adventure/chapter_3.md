# Chapter 3 - Making money

<img src="./assets/cover_3.png">

> In this chapter we implement a token for our DAO. This is an essential step to make our project economically sustainable. A mistake commonly made when creating a DAO is to believe that having a token is enough to guarantee a solid business strategy and consistent income for the organization - this is not the case.

## Introduction

Creating and distributing a token is an essential step in any DAO. A token enables the creation of a market, enabling investors to invest in the DAO, community members to receive rewards for their contributions, and usually facilitates governance by allowing token holders to vote on key decisions and initiatives. Today, your mission, is to implement the code for a token.

On the Internet Computer, we can create a token by creating a canister that stores balances and manage transfer. Assuming the canister is not controlled we can consider the token to be safe, trustless and decentralized. In this project you will implement the code for a simple token. If you are interested in learning more about tokens, you can read the [ICRC_1 standard](https://internetcomputer.org/docs/current/developer-docs/integrations/icrc-1).

## Resources

To complete this Chapter, we suggest browsing the following resources:

<ul>
  <li><a href="https://internetcomputer.org/docs/current/motoko/main/base/Option" target="_blank">Option module </a></li>
  <li><a href="https://internetcomputer.org/docs/current/motoko/main/base/Principal" target="_blank">Principal module </a></li>
</ul>

## Tasks

1. Define the `ledger` variable. This variable will be used to store the balance of each user. The keys are of type `Principal` and the values of type `Nat`. You can use the `HashMap` or `TrieMap` types to implement this variable.
2. Implement the `tokenName` function, this function takes no parameters and returns the name of your token as a `Text`.

> Choose any name you want for your token.

3. Implement the `tokenSymbol` function, this function takes no parameters and returns the symbol of your token as a `Text`.

> Choose a symbol that is exactly 3 characters in length.

4. Implement the `mint` function. This function takes a `Principal` and a `Nat` as arguments. It adds the `Nat` to the balance of the given `Principal`. You will use the `Result` type for your return value.
5. Implement the `burn` function. This function takes a `Principal` and a `Nat` as arguments. It subtracts the `Nat` from the balance of the given `Principal`. You will use the `Result` type for your return value.
6. Implement the `transfer` function. This function takes a `Principal` representing the sender (from), a `Principal` representing the recipient (to), and a `Nat` value for the amount to be transferred. It transfers the specified amount of tokens from the sender's account to the recipient's account. You will use the `Result` type for your return value.
7. Implement the `balanceOf` query function. This function takes a `Principal` as an argument and returns the balance of the given account as a `Nat`. It should return 0 if the account does not exist in the `ledger` variable.
8. Implement the `totalSupply` query function. This function takes no parameters and returns the total supply of your token as a `Nat`. The total supply is calculated by adding together the balances of every user stored in the `ledger` variable.
9. Complete **Chapter 3** by deploying your canister and submitting your ID on [motokobootcamp.com](https://www.motokobootcamp.com/).

> To deploy your application run `dfx deploy --playground chapter_3`.

## Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/dX3c5-YcNi4?si=dc8Le4njcr_wULds" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" style="display: block; margin-left: auto; margin-right: auto;"></iframe>

> ⚠️ Please be aware: the repository displayed in the video may not match the one you're working with, due to recent updates we've made to the repository which have not been reflected in the video. However, the core code should remain similar.
