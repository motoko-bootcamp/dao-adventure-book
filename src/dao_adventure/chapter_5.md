# Chapter 5 - Build your brand

<img src="./assets/cover_5.png">

> In this chapter we will build a website and an identity for our DAO. This important step enables us to increase our visibility in the ecosystem and bring people that share the same vision together.

## Introduction

Up until now, we've been working behind the scenes, mainly because Motoko is a language designed for backend development. Today, we're going to create a website for our DAO. We'll take advantage of canisters' ability to store assets and directly handle incoming HTTP requests to serve websites. When it comes to building a website on the Internet Computer, we have two main options:

Use the asset canister and make use of familiar frontend technologies like HTML, JavaScript, CSS, and any frameworks you like.
Build the website from the Motoko side by implementing the http_request query method.
Actually, these two approaches end up being similar. This is because the asset canister essentially uses the http_request method behind the scenes to serve web content but abstract away this complexity for the developer.

## Resources

To complete this Chapter, we suggest browsing the following resources:

<li><a href="https://nnri3-7qaaa-aaaaj-qa3qa-cai.icp0.io/motoko_theory/lesson-13/lesson-13.html" target="_blank">Lesson 13 - Serving a webpage </a></li>

## Tasks

1. Select a logo for your DAO. You will need to find a logo that is available as an SVG file. You can use a website like [FlatIcon](https://www.flaticon.com/fr/).

> SVG stands for Scalable Vector Graphics. We will use SVGs because they are basically text files that carry vector information about visuals. This means we don't have to worry about uploading any asset to our canister, we can simply copy the SVG file and paste it directly in our code.

2. Set the value of the immutable variable called `logo` of type `Text` to the value of the logo.

> You can copy the content of the SVG file and paste it directly into your code. Ensure that you use single quotes (`) for any quotes within the SVG file and double quotes (") for enclosing the entire text, as Motoko employs double quotes to delineate strings.

3. Implement the `getStats` function. This function will be used to display some statistics about your DAO.

In Motoko, to serve a webpage, you simply need to implement a http_request query function. This function will be called by the Internet Computer when a user tries to access your webpage.
For instance this is how you would implement a simple http_request function that returns a simple `Hello World` webpage:

```motoko
public query func http_request(request : HttpRequest) : async HttpResponse {
    let response = {
        body = Text.encodeUtf8("Hello world");
        headers = [("Content-Type", "text/html; charset=UTF-8")];
        status_code = 200 : Nat16;
        streaming_strategy = null
    };
    return(response)
}
```

4. Implement the `http_request` query function. This function will be used to serve the webpage of your DAO. You can use the `_getWebpage` function to generate the HTML of the webpage.

## Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/b7OFEP_SKME?si=ZlhRbrvVy8aPMsA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" style="display: block; margin-left: auto; margin-right: auto;"></iframe>

> ⚠️ Please be aware: the repository displayed in the video may not match the one you're working with, due to recent updates we've made to the repository which have not been reflected in the video. However, the core code should remain similar.
