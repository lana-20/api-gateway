# API Gateway Overview

<img src="https://user-images.githubusercontent.com/70295997/206981096-afea95c7-5d37-4755-97e2-64e9db237a94.png" width=600>

I need to build an Abstraction Layer. There is no reason for the UI developer to know every Microservice (MS) I have in the Backend. This Layer acts as a facade. It does nothing on its own, except it routes the requests and responses made outside my MS system. I provide my UI/UX developer with this Abstraction Layer.

The Abstraction Layer has all the APIs I want exposed to the outside world. And when the request comes in, it knows which MS to call. In that sense, the Abstraction Service acts as the traffic controller or a router. It forms a single entry point for all the MSs.

With the Abstraction Service in place, I am now free to split my Backend into as many MSs as I like or refactor them as many times as I like. And I have them communicating with each other internally however I like.

As long as everything is in the contract of this 'facade' service, everyone who's accessing my API from the outside doesn't need to know what I'm doing within. This 'facade' layer is called the __API Gateway__. It's a gateway (GW) at the very edge of my MS architecture diagram. As a result, it's sometimes referred to as __Edge Microservice__.

### How to start using an API Gateway?

First, identify external API. Every MS has REST API of its own, but I don't want them all to be accessible to the outside world.

__What are the APIs that I'm ok with people calling?__

_External API Contract_

<img src="https://user-images.githubusercontent.com/70295997/207100458-7a3798ae-eab1-4dbd-9142-9736f0f03408.png" width=800>

What's that Contract going to look like? First, I design/craft my APIs. Then I bring in this MS that acts as a Gateway. I either write my own or use one of the available technologies. I basically create a bunch of APIs in accordance with this public API that I decided to expose. All it does internally is calling one of my existing MSs and passing along the response. This technique is called __API Composition__. I compose an API out of other existing APIs.

Since now I have a single point of entry that all my requests need to go through, there is a number of other things I can take advantage of. Eg, add a Monitoring system that measures how many requests come in, how long they take, etc. This is great for the Operation and Support teams.

<img src="https://user-images.githubusercontent.com/70295997/207110363-3b56be18-d8f5-4e91-a7e9-067c6b453a64.png" width=800>

I can Authenticate a user here, pass security tokens like JWT, implement security measures and prevent things like Denial of Service attacks, prevent access to certain users and IPs, etc. If I end up needing to do all this stuff, then I may consider not writing my own API and looking at other existing technologies. There a bunch of options to choose from.

__Open source API Gateway Implementations__

One popular choice is the API GW Implementation from the Netflix MS stack called Zuul. I download and configure Zuul and run it whenever my MSs run. And that then acts as my API GW.

<img src="https://user-images.githubusercontent.com/70295997/207111137-54291333-2ff2-4761-86b2-eea86d3be982.png" width=600>

There are other options, including hosted implementations like AWS. No matter which one I use, the pattern is more or less the same.

__Disadvantages of using API GW pattern__

1. I add a Network Hub here. Things may slow down, there's nothing I can do about it since the pattern requires it.
<img src="https://user-images.githubusercontent.com/70295997/207112873-ba7cbe49-5c53-4832-802f-a3de327606ec.png" width=600>

2. How many of these API GWs do I need? Do I just create one? One can be a problem. I build MSs with fault tolerance and redundancy in mind, so even if some of these instances were to go down, the system would still function. What if my API GW goes down? As it's a single entry point, the whole system goes down as well. I can create multiple API GWs and split my incoming calls to them using, eg, a Load Balancer or Elastic IPs.

<img src="https://user-images.githubusercontent.com/70295997/207124826-678ed2e6-2e72-4730-a20d-9122dc271490.png" width=800>

3. API GW can technically get a bit compliicated. Let's say I have a Web client for my MSs, and I have an Android team and an iOS team. These are completely different APIs and configurations. In that case, instead of overcomplicating one single GW, I can create multiple types of API GWs - one for each client type. I can have those clients call the right API GW or configure Load Balancers that route requests to the right API GW.

<img src="https://user-images.githubusercontent.com/70295997/207126754-5a6bea63-4bab-40d2-b849-71d3e51379d8.png" width=600>

__Backend for Frontend Pattern__

I create a Backend endpoint for the Frontend that's calling it. Frontend developers use my API GW as the one endpoint that they need to call. Once they refactor al their code to call my GW, I'm free to do whatever I like in my MS Architecture. As long as I observe the _External API Contract_.


----

[What is an API Gateway? - IBM](https://youtu.be/hWRRdICvMNs)

