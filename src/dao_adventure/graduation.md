# Graduation

<img src="./assets/cover_graduation.png">

> In this final chapter, we will build our graduation project. The end goal is to build a webpage where the text displayed is entirely controlled by a DAO. This project showcases the possibility of building community-owned web applications. Think of the webpage as just a starting point to show what else could be run by a DAO – like an entire game, a social network, an app, or even an AI model.

## Introduction

Until now, we've only worked with applications that use a single canister. Today, we'll learn how to build an application that uses more than one canister. In this final project, you'll be working with three different canisters:

- The DAO canister, which contains the profile of your members, the logic for registration, and the voting system.
- The token canister, which contains the logic for the Motoko Bootcamp Token, stores balances and manages transfers.
- The webpage canister, which contains and serves your live webpage.

> We could have combined all the functions of these three canisters into one to make the project simpler. However, we chose to use three separate canisters for a couple of reasons. First, by having everyone use the same token canister, all the DAOs (the decision-making tools) are linked financially. Second, we want to demonstrate how you can control one canister from another (using the DAO canister to manage the others). This is an important concept for creating self-managing applications and exploring new possibilities for your projects.

## Requirements

1. **Membership and Token Allocation**

- New members receive 10 Motoko Bootcamp Tokens (MBT) upon joining.
- MBTs are used for participating in DAO activities.

2. **Role System**

- The DAO comprises three roles: Students, Graduates, and Mentors.
- Students: All members start as students. They are members who haven't completed the Motoko Bootcamp.
- Graduates: These are members who have completed the Motoko Bootcamp. They gain the right to vote on proposals. Any member can become a Graduate through a graduate function, which only a Mentor executes. There's no need to implement a verification process for this.
- Mentors: Graduates who are selected by the DAO become Mentors. They can both vote on and create proposals. An existing Mentor can assign the Mentor role to any Graduate member by creating a proposal. This proposal has to be approved by the DAO.

3. **Proposal Creation**

- Only **Mentors** are authorized to create proposals.
- To create a proposal, a **Mentor** must burn 1 MBT, which decreases their token balance.

4. **Voting System**

- Only Graduates and Mentors are allowed to vote.
- The voting power of a member is determined as follows:
- If the member is a **Student** - the voting power is set to 0 (**Student** don't have voting power).
- If the member is a **Graduate** - his voting power is directly equal to the number of MBC token they hold at the moment of voting.
- If the member is a **Mentor** - his voting power is equal to 5x the number of MBC tokens they hold at the moment of voting.
- The `yesOrNo` field of the Vote object is a `Bool` representing whether a vote is meant to approve or refuse a proposal. `true` represents a vote in favor of a proposal and `false` represents a vote against a proposal.

- When a member votes on a proposal, his voting power is added or subtracted to the `voteScore` variable of the `Proposal` object.

- A proposal is automatically accepted if the `voteScore` reaches 100 or more. A proposal is automatically rejected if the `voteScore` reaches -100 or less. A vote stays open as long as it's not approved or rejected.

- Approved proposals are automatically executed.

> For example, if a mentor possessing 15 Motoko Bootcamp Tokens (MBT) casts a vote in favor of a proposal (true), their vote contributes 75 to the voteScore due to the 5x multiplier for mentors' votes. If the voteScore before this vote was 30, it would increase to 105 after the vote is counted. Consequently, the proposal reaches the acceptance threshold and is successfully implemented.

5. **Proposal Types**
   There are 2 types of proposals:

- `ChangeManifesto`: those proposals contain a `Text` that if approved will be the new manifesto of the DAO. If the proposal is approved the changes should be reflected on the DAO canister and the Webpage canister.
  `AddMentor`: those proposals contain a Principal that if approved will become a mentor of the DAO. Whenever such a proposal is created, we need to verify that the specified principal is a Graduate of the DAO, as only Graduate can become Mentors. If the proposal is approved the changes should be reflected on the DAO canister.

6. **Initial Setup**
   The initial setup of the DAO should include an initial mentor to ensure that your DAO is operational:

- Mentor:
  - Name: `motoko_bootcamp`
  - Associated Principal: `nkqop-siaaa-aaaaj-qa3qq-cai`

> You can decide to hardcode the initial setup or create an external one that will be executed upon canister deployment.

7. **Token Faucet**
   You are required to use the **Motoko Bootcamp Token**, a free, educational token faucet. It allows unlimited minting but holds no real economic value; it's solely for educational use.

Find the token faucet source code in the [token](https://github.com/motoko-bootcamp/dao-adventure/blob/main/chapters/graduation/token/main.mo) folder. Deploy it locally for building and testing. For your live project on the Internet Computer, you are required to use the existing token faucet on the Internet Computer with the canister ID `jaamb-mqaaa-aaaaj-qa3ka-cai`.

Access the interface of the deployed token faucet canister [here](https://dashboard.internetcomputer.org/canister/jaamb-mqaaa-aaaaj-qa3ka-cai).

You'll need to use the Faucet canister to:

- Mint tokens when a new member joins your DAO.
- Burn tokens when a new proposal is created.

## Resources

To complete this Chapter, we suggest browsing the following resources:

<li><a href="https://nnri3-7qaaa-aaaaj-qa3qa-cai.icp0.io/motoko_theory/lesson-13/lesson-13.html" target="_blank">Lesson 11 - Intercanister calls </a></li>

## Submission

As with previous chapters, you'll need to submit your project on the [Submission website](https://www.motokobootcamp.com/). For that project, **you need to submit the canister ID of the DAO canister.**

Upon submitting your project, to determine if you have graduated or not, a few tests will be automatically performed on your **DAO canister**. Those tests will take between 20 and 30 seconds.

1. Do not interact with the **DAO canister** during the testing phase.
2. Strictly respect the interface and types that are defined and provided in this repository. Any modification will result in a failed test.
3. If your test fails without prompting an error message or loads for more than 1 minute, open your browser inspector, click on the developer console, take a screenshot, and report the issue in our [feedback channel](https://discord.gg/vTcwUdUwTf).

## Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/onwvvi5EUi8?si=UVEVFXB7PUegQeuJ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" style="display: block; margin-left: auto; margin-right: auto;"></iframe>

> ⚠️ Please be aware: the repository displayed in the video may not match the one you're working with, due to recent updates we've made to the repository which have not been reflected in the video. However, the core code should remain similar.
