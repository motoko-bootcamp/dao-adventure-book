# Introduction to Motoko

## A board to greet students 👋

In this introduction, we aim to design a welcoming board that displays messages to greet students joining the Academy. This board is unique in that it can only hold one message at a time. To view the current welcome message, students must themselves contribute by writing a new message for the next student. Additionally, the board stores the total number of messages that have been printed.

## Actor

If you open a Motoko file, there is a high probability that the first word you encounter is `actor`:

```motoko
actor {

}
```
An **actor** is how a **canister** is defined in **Motoko**. This terms comes from the [Actor model](https://doc.akka.io/docs/akka/current/typed/guide/actors-intro.html) - a theory on how to design systems that can handle multiple tasks concurrently.

Think of an **actor** as a small robot that can receive messages, do some work and then send messages to other **actors**. **Actors** can also instantiate new **actors**. All the **actors** talk to each other by sending messages but they can't access the state of each other directly.

> For instance, an external canister looking to access the value of the current welcoming message would have to do it through a message - also called inter-canister call.

You can choose to give your **actor** a name if you want, by writing the name right after the word `actor`.

```motoko
actor Board {

}
```

## Variables and Types
Inside the body of the actor we can define variables. In Motoko, variables are grouped into two categoies: immutable and mutable.

- Immutable variables are variables that cannot be changed after they have been assigned a value. The `let` keyword is used to define an immutable variable in Motoko.

> For instance, your name would be an immutable variable since it's unlikely to change.

- Mutable variables are variables that can be changed after they have been assigned a value. The `var` keyword is used to define a mutable variable in Motoko.

> For instance, your age would be a mutable variable since it would likely change - every year.

For our Board project, we need to define a variable to store the current message and another one to store the total number of printed message. In Motoko, every variable has a specific type. This is a crucial aspect of Motoko because it helps avoid mistakes by ensuring that variables of different types cannot be combined or confused.

> For instance, you wouldn't be able to add a variable of type `Text` with a variable of type `Nat`.

- Our stored message will be a mutable variable of type `Text`.
- The counter will be a mutable variable of type `Nat`.
```motoko
var message : Text = "Motoko Bootcamp will become the best Web3 bootcamp in the world!";
```
The `:` is used to specify the type of the variable. In this case, we are using the `Text` type, which is a built-in type in **Motoko** for representing text strings.

```motoko
var counter : Nat = 0;
```
In our second variable, we are using the **Nat** type, which is a built-in type in Motoko for representing natural numbers (0, 1, 2, 3...)

## Functions
> In this example, we will only define public functions. Those functions can be accessed by anyone and are part of the public interface of the canister. We will see later in the course how to define private functions.

Just like we have two types of variables, we also have two types of functions:

### Update
Update calls are used when the user wants to modify the state of a canister. To ensure the integrity of the Internet Computer, these calls must be processed through consensus and by all nodes, which results in a delay of around 2-3 seconds. An update call would be used in the following situations:

- Posting on a social media, such as [DSCVR](https://dscvr.one/).
- Sending a message on a messaging application, such as [OpenChat](https://oc.app/).
- Buying a NFT on [Entrepot](https://entrepot.app/).

In Motoko, every function is an update function by default, unless specified otherwise using the `query` keyword (more on that in the next section).

We are developing a function for our Board to show the latest message. Each time a student uses this function, they must submit a new message. This design ensures that the Board displays the previous message only after a new one is entered, guaranteeing there is always a message for the next student to see.

```motoko
public func showMessage(newMessage : Text) : async Text {
    let oldMessage = message;
    message := newMessage;
    counter += 1;
    return oldMessage;
};
``` 

Just like variables, arguments and return values of functions have types. In our example, the `showMessage` function takes a `Text` type as an argument and returns a `Text` type. The `async` keyword means the function is asynchronous and returns a promise that will eventually be fulfilled with the function's outcome. In general every function that is part of the public interface of a canister  is asynchronous. If you are not familiar the concept of **promises** and `async/await` - take a look at [this video](https://www.youtube.com/watch?v=vn3tm0quoqE) explaining this concept for the **JavaScript** language, it's the same concept in **Motoko**.

### Query
Query calls are used when a user wants to read data without modifying the state. These calls can be answered by a single node, making them very fast (at around **200ms**). The downside is that query calls are less secure as a malicious node could potentially provide false information. A query call would be used in the following situations:

- Reading an article on [Nuance](https://nuance.xyz/).
- Checking your user profile picture on [DSCVR](https://dscvr.one/).
- Loading a video or a picture on any platform on [Taggr](https://taggr.link/)

In **Motoko**, we define `query` functions by using the `query` keyword.

For our **Board**, we want to define a query function that returns the total number of printed messages.

```motoko
public query func getNumberMessage() : async Nat {
    return counter;
};
``` 

## Deploying a Canister
To deploy a canister, we will use the dfx command line tool.

```bash
dfx deploy --playground qualification_demo
```

This command deploys the canister to the **Internet Computer** using the `dfx.json` file. Within `dfx.json`, we specify the canister's name and the main Motoko's entry point. The entry point is the **Motoko** file hosting the `actor` along with public functions, forming the canister's public interface.
```json
{
  "canisters": {
    "qualification_demo": {
      "main": "src/qualification/demo.mo",
      "type": "motoko"
    }
  }
}
```

Interacting with a Canister (Candid UI)
WIP

Interacting with a Canister (Frontend)
WIP

