# Chapter 1 - What is your dream?

<img src="./assets/cover_1.png">

> In this Chapter, we are setting the foundation for your DAO. We will define its name, its objectives, and we will also craft a manifesto describing its guiding principles and vision.

## Introduction

DAOs represent an entirely new way to fuel your dreams. Think about it - this is the first time that anyone can collaborate with the entire world without the need to travel, learn multiple languages or sign any contract - everything happens through the blockchain.

Whether you are passionate about Web3, AI, music, economy, open source, 3D printing or even politic - DAOs have something for you. You need to figure out what and how you to leverage this new technology. Let your imagination go wild, we are at the beginning of a new era. Now is the time to dream big and experiement crazy ideas.

Today, we're going to outline a vision, choose a name, and set goals for our DAO. If you have an existing project, think about adding a community aspect to it to form our DAO. If you don't have a project, think about any club you've liked or ever wanted to join. We'll use these to create our DAO.

## Resources

To complete this Chapter, we suggest browsing the following resources:

<ul>
  <li><a href="https://nnri3-7qaaa-aaaaj-qa3qa-cai.icp0.io/motoko_theory/lesson-1/lesson-1.html" target="_blank">Lesson 1 - Fundamental concepts</a></li>
  <li><a href="https://nnri3-7qaaa-aaaaj-qa3qa-cai.icp0.io/motoko_theory/lesson-2/lesson-2.html" target="_blank">Lesson 2 - Programming concepts</a></li>
  <li><a href="https://nnri3-7qaaa-aaaaj-qa3qa-cai.icp0.io/motoko_theory/lesson-3/lesson-3.html" target="_blank">Lesson 3 - Primitives types</a></li>
  <li><a href="https://nnri3-7qaaa-aaaaj-qa3qa-cai.icp0.io/motoko_theory/lesson-4/lesson-4.html" target="_blank">Lesson 4 - Candid</a></li>
  <li><a href="https://internetcomputer.org/docs/current/motoko/main/base/Buffer" target="_blank">Buffer</a> or the subsection Buffer of <a href="https://nnri3-7qaaa-aaaaj-qa3qa-cai.icp0.io/motoko_theory/lesson-6/lesson-6.html#-buffer" target="_blank">Lesson 6 - Data-structures</a></li>
</ul>

## Tasks

> To complete this project - you need to make use of the Buffer library in Motoko. Make sure that you've read the corresponding documentation.

1. Define an immutable variable `name` of type `Text` that represents the name of your DAO.
2. Define a mutable variable `manifesto` of type `Text` that represents the manifesto of your DAO.

> A manifesto is a public declaration of the intentions, motives, or views of an individual or group. It is often political in nature, but may present an individual's life stance.

3. Implement the `getName` query function, this function takes no parameters and returns the name of your DAO.
4. Implement the `getManifesto` query function, this function takes no parameters and returns the manifesto of your DAO.
5. Implement the `setManifesto` function, this function takes a newManifesto of type `Text` as a parameter, updates the value of manifesto and returns nothing.
6. Define a mutable variable goals of type `Buffer<Text>` will store the goals of your DAO.
7. Implement the `addGoal` function, this function takes a goal of type `Text` as a parameter, adds a new goal to the goals buffer and returns nothing.
8. Implement the `getGoals` query function, this function takes no parameters and returns all the goals of your DAO in an Array.
9. Complete **Chapter 1** by deploying your canister and submitting your ID on [motokobootcamp.com](https://www.motokobootcamp.com/).

> To deploy your application `dfx deploy --playground chapter_1` (remember to paste this command in a new terminal).

## Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/Xkr90-923LU?si=yjEVyecY1tMk9zO6" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" style="display: block; margin-left: auto; margin-right: auto;"></iframe>

> ⚠️ Please be aware: the repository displayed in the video may not match the one you're working with, due to recent updates we've made to the repository which have not been reflected in the video. However, the core code should remain similar.
