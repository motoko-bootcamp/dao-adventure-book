# Chapter 2 - Create your tribe

<img src="./assets/cover_2.png">

> In this chapter we will make it possible for others to join our DAO. For that, we will implement CRUD (Create, Read, Update, Delete) functionalities inside our canister.

## Introduction

The key element of any DAO is its community. This community unites over shared interests, objectives, and often a vision for the future. Typically, in a DAO, members are active participants: they engage in decision-making, contribute to the DAO, and can even receive compensation for their contributions.

Today, we won't focus on building the community itself (this could take months). Instead, we'll concentrate on the technical side, setting up a system to enroll members into our application and keep track of some basic information about them.

## Resources
WIP

## Tasks
> To complete this project - you need to make use of the `HashMap` and `Result` library in Motoko. Make sure that you've read the corresponding chapter.

To help you get started, we've defined different types in [main.mo]():

- A new type `Member` to represent the members of your DAO.
```motoko
type Member = {
    name: Text;
    age : Nat;
};
```
- A new type `Result` that we've imported from the **Result** library. This type will be used to return potential errors from your functions.
```motoko
type Result<A,B> = Result.Result<A,B>;
```
- A type `HashMap` that we've imported from the **HashMap** library. This type will be used to store the members of your DAO.
```motoko
type HashMap<K,V> = HashMap.HashMap<K,V>;
```
1. Define an immutable variable members of type `Hashmap<Principal,Member>` that will be used to store the members of your DAO.
> You might be wondering why we're using an immutable variable in this context, especially when we plan to add members to the data structure. The reason for this choice is that we are using a HashMap, and our intention is not to change the reference to the HashMap itself, but rather to modify the content within the HashMap.

2. Implement the `addMember` function, this function takes a `member` of type `Member` as a parameter, adds a new member to the `members` HashMap. The function should check if the caller is already a member. If that's the case use a `Result` type to return an error message.
3. Implement the `getMember` query function, this function takes a `principal` of type `Principal` as a parameter and returns the corresponding member. You will use a `Result` type for your return value.
4. Implement the `updateMember` function, this function takes a `member` of type `Member` as a parameter and updates the corresponding member associated with the caller. If the member doesn't exist, return an error message. You will use a `Result` type for your return value.
5. Implement the `getAllMembers` query function, this function takes no parameters and returns all the members of your DAO as an array of type `[Member]`.
6. Implement the `numberOfMembers` query function, this function takes no parameters and returns the number of members of your DAO as a `Nat`.
7. Implement the `removeMember` function, this function takes no parameter and removes the member associated with the caller. If there is no member associated with the caller, return an error message. You will use a `Result` type for your return value.
8. Complete Chapter 2 by deploying your canister and submitting your ID on [motokobootcamp.com](https://www.motokobootcamp.com/).

> To deploy your application run `dfx deploy --playground chapter_2`.

## Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/8TVEVfPDJnw?si=dc8Le4njcr_wULds" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" style="display: block; margin-left: auto; margin-right: auto;"></iframe>