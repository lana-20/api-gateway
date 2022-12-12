# API Gateway

<img src="https://user-images.githubusercontent.com/70295997/206981096-afea95c7-5d37-4755-97e2-64e9db237a94.png" width=600>

I need to build an Abstraction Layer. There is no reason for the UI developer to know every Microservice (MS) I have in the Backend. This Layer acts as a facade. It does nothing on its own, except it routes the requests and responses made outside my MS system. I provide my UI/UX developer with this Abstraction Layer.

The Abstraction Layer has all the APIs I want exposed to the outside world. And when the request comes in, it knows which MS to call. In that sense, the Abstraction Service acts as the traffic controller or a router. It forms a single entry point for all the MSs.

With the Abstraction Service in place, I am now free to split my Backend into as many MSs as I like or refactor them as many times as I like. And I have them communicating with each other internally however I like.

As long as everything is in the contract of this 'facade' service, everyone who's accessing my API from the outside doesn't need to know what I'm doing within. This 'facade' layer is called the __API Gateway__. It's a gateway at the very edge of my MS architecture diagram. As a result, it's sometimes referred to as __Edge Microservice__.

### How to start using an API Gateway?

First, identify external API. Every MS has REST API of its own, but I don't want them all to be accessible to the outside world.

__What are the APIs that I'm ok with people calling?__

_External API Contract_

GET		/user

POST	/user

GET		/cart/<id>
  
PUT		/cart
  
POST	/cart
  
...		



