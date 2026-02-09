## From prototype to production: A low-latency multiplayer stack on a tight budget

When you start working on a real-time multiplayer game, the idea might seem simple, but it can escalate quickly. That happened when we started giving form to Rumble Racer with the Blyts team.

<h2>The challenge</h2>

Rumble Racer is an online multiplayer racing game for mobile that mixes Subway Surfers-style controls with popular arcade racing games. It’s a four-player racing game that ended up being very fun to play.

The challenge was to achieve a production-ready server infrastructure to host worldwide matches, keeping an eye on the infrastructure budget and providing high availability.

In the prototype stage, we choose <a href="https://mirror-networking.com/">Mirror</a> as a networking engine for both matchmaking and gameplay. Mirror was a great match as it was open-source and had a great community on Discord, giving me the ability to extend the library as needed in the long run.

For production, using Mirror for matchmaking in the lobby has its flaws. Mirror runs Unity on a dedicated server and works perfectly, but as the matches add up it starts consuming CPU on the Linux box, requiring more instances and dividing players into batches per server. That limits matchmaking to the players connected to that server.

Also, due to the requirement to support worldwide players, and the low latency needed to keep a smooth real-time experience for everyone, regional servers were required.

<h2>Server architecture</h2>

So after some thought, I designed and implemented the server architecture as follows: a .NET lobby server in each region communicating using SignalR, and multiple Mirror servers connected to each lobby server. This provides a high-availability, scalable architecture to support as many players as required, with low latency and region-scoped matchmaking, while keeping Mirror for match simulation, where headless Unity shines.

<img src="/assets/rr-architecture.png" alt="server architecture diagram" />

<h2>Final game flow</h2>

The client connects to a master lobby server on start, downloading an updated list of servers. On the first connection, the servers are latency tested, choosing the fastest responder. Once connected, matchmaking takes place on the lobby server with all the players from that region, allowing a seamlessly integrated experience. 

When the four players are ready, the lobby server acts as a load balancer, choosing a Mirror server to host the race and sending, via a REST API, the race info and the players’ info, then sharing that server’s details with each player so they can connect and start the race.

All servers are deployed on Linux machines using Docker containers, and we’re ready to add Kubernetes to the mix when traffic requires it, to provide real-time flexibility in the infrastructure.

You can find links to the store and more info about the game in the <a href="/portfolio">portfolio section</a>.


