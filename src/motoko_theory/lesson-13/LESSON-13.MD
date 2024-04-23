# Lesson 13: Accessing to a canister through our browser.

## Difference between HTTP request & HTTP outcalls.

In this lesson, we will cover how canisters can be accessed through HTTP requests. This is a separate topic from **HTTP Outcalls**:

- **HTTP Request**: Canisters can handle incoming requests and serve web pages.
- **HTTP Outcalls**: Canisters can send requests and communicate with the Web 2.0 world. This can be used for various use cases, such as querying an exchange for token prices, getting the latest weather information, and sending notifications to users.

Whenever you [access a canister](https://wujxq-qqaaa-aaaaj-qazca-cai.raw.ic0.app/) through your browser there are a few steps involved. Let's go through all of them.
You will notice that URLs on the Internet Computer are of the following form: `<CANISTER_ID>.ic0.app`.
`.ic0.app` indicates that you are reaching out to boundary nodes.

## What are boundary nodes?

Canisters are hosted and executed by nodes that participate in the IC consensus However, those nodes are not directly accessible by end users.
To protect the consensus nodes & improve performance there is a layer of boundary nodes which serve different useful purposes:

- Translate the HTTP request of the user's browser to canister call. This part is called the HTTP Gateway protocol. When canisters send their response the gateway will convert it back to an HTTP request.
- Route the calls to the correct subnet running the canister. To properly route those calls the boundary nodes have to keep track of the entire configuration of the Internet Computer:
  - List of subnets.
  - List of nodes and which subnet they belong to.
  - The canisters run by each subnet.
- Load balancing among the subnet's replica nodes (i.e if a replica is lagging behind and has already a lot of work on its plate - boundary nodes will send the request to another replica).
- Protect subnets from DDoS attacks.

<p align="center"> <img src="./assets/http_gateway.png" width="800px" style="border: 2px solid black;"> </p>

> Currently, boundary nodes are run by the DFINITY Foundation. However, the objective ([as part of the roadmap](https://forum.dfinity.org/t/boundary-node-roadmap/15562)) is to have anyone able to set up and run a boundary nodes. This will make interaction with the Internet Computer more reactive for end users and this will make the platform more robust to censorship.

## The asset canister

To serve web content on the Internet Computer, a canister should have a method that can handle an `http_request`, which includes the URL, HTTP method, and headers, and produce an HTTP response, consisting of a status, headers, and body. There are two ways to go about that:

- Implement the http_request method and all associated logic yourself.
- Use the provided **asset** canister: this is a special canister whose code has been already implemented by DFINITY. You need to specify the type of this canister in `dfx.json` & add the source folder of your web app. Once the asset canister is deployed on the Internet Computer the website can be accessed at `http://<canister id>.ic0.app` and `http://<canister id>.raw.ic0.app` (the raw domain without certification). The frontend canister that is shipped when you deploy a project with `dfx new <project>` is an asset canister (as you can confirm by looking at `dfx.json`).

> You can access [the source code for this canister written in Rust](https://github.com/dfinity/sdk/tree/master/src/canisters/frontend/ic-frontend-canister) under the [DFINITY organization](https://github.com/dfinity).

## The `http_request` query method

Once the boundary node has received the request. It will encode it into Candid and automatically call the `http_request` method of the canister. reachable by browsers, you need to implement an `http_request` query method as part of the public interface of your actor. <br/>

```motoko
import Text "mo:base/Text";
import Http "http";
actor {
    public type HttpRequest = Http.HttpRequest;
    public type HttpResponse = Http.HttpResponse;

    public query func http_request(req : HttpRequest) : async HttpResponse {
        return({
            body = Text.encodeUtf8("Hello World");
            headers = [];
            status_code = 200;
            streaming_strategy = null;
        });
    };
};
```

Here is the content of the `HTTP` module, the file name is `http.mo`.

```motoko
module Http {
    public type HeaderField = (Text, Text);

    public type HttpRequest = {
        body: Blob;
        headers: [HeaderField];
        method: Text;
        url: Text;
    };

    public type HttpResponse = {
        body: Blob;
        headers: [HeaderField];
        status_code: Nat16;
        streaming_strategy: ?StreamingStrategy;
    };

    public type StreamingStrategy = {
        #Callback: {
            callback : StreamingCallback;
            token    : StreamingCallbackToken;
        };
    };

    public type StreamingCallback = query (StreamingCallbackToken) -> async (StreamingCallbackResponse);

    public type StreamingCallbackToken =  {
        content_encoding : Text;
        index            : Nat;
        key              : Text;
    };

    public type StreamingCallbackResponse = {
        body  : Blob;
        token : ?StreamingCallbackToken;
    };
}
```

Once the method is implemented, you can access [the webpage served by the canister](https://wujxq-qqaaa-aaaaj-qazca-cai.raw.ic0.app/).

<p align="center"> <img src="./assets/hello_world.png" width="800px" style="border: 2px solid black;"> </p>

If you access the canister, through the [Candid UI](https://a4gq6-oaaaa-aaaab-qaa4q-cai.raw.ic0.app/?id=wujxq-qqaaa-aaaaj-qazca-cai) you will notice that the `http_request` is indeed present.

<p align="center"> <img src="./assets/candid_ui.png" width="800px" style="border: 2px solid black;"> </p>

The content of the webpage can be dynamically modified based on the state of the canister - leave your name!
