# Chapter 4 - Listen to your community

<img src="./assets/cover_4.png">

> In this chapter we implement a voting system. A voting system enables the community to take important decisions together on the future of the DAO. Governance is a complex area and many different type of governance model could be implemented depending on the need of the organization.

## Introduction
Decentralized organizations are often critized for they lack of efficiency. A common misconception is that all DAO decisions require a vote from every member. This is both inefficient, frustrating, and unnecessary. The secret of DAOs lies in the subtle balance between efficiency, pragmastim and transparency. <br/>

Organizations with different purposes will likely require different types of governance.

Technology is on our side. We can create and refine any governance system based on outcomes, allowing us to conduct experiments and learn from them.

Today, for simplicity, we'll set up a basic, non-realistic voting system that meets these requirements

- Only allow members of the DAO to vote and create proposals.
- The voting power of each member should be equal to the number of tokens they hold.
- Creating a proposal should require to burn 1 token.
- A member can only vote once per proposal.
- Everytime a member votes, the score of the proposal is updated. Depending on whether or not the member voted for or against the proposal, the score should be increased or decreased by the member's voting power. For instance, if a member with 10 tokens votes for a proposal, the score should be increased by 10. If the same member votes against the proposal, the score should be decreased by 10.
- A proposal is automatically approved if the score reaches 100 or more. A proposal is automatically rejected if the score reaches -100 or less. Otherwise the proposal is still open to voting.
- Any approved proposal should be automatically executed by the DAO.

## Resources
To complete this Chapter, we suggest browsing the following resources:

<li><a href="https://internetcomputer.org/docs/current/motoko/main/pattern-matching" target="_blank">Pattern matching</a></li>


## Tasks

> To get started, we've provided various types in types.mo. Ensure you don't alter these types, as changes will cause the test to fail.

1. Create a datastructure to store the proposals.
2. Implement the `createProposal` function. If the proposal is successfully created, the function should return the id of the proposal.
3. Implement the `getProposal` function.
4. Implement the `voteProposal` function.
5. Implement the `getAllProposals` function.

## Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/WKxP6gxjaSQ?si=yyjDWrZXCWWhhX7P" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" style="display: block; margin-left: auto; margin-right: auto;"></iframe>