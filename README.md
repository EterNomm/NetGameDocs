# NetGameDocs
Lists of useful documentation for creating a multiplayer game

## Why i created this
Well, multiplayer is hard to create, ngl. Thats why i created this repo to help anybody who wants to make a networked game
This can be very helpful if your game is server side, meaning that server is the one who did every logic, and the client just visualizes it

### The problem with latency
So, basically, networking is pretty complicated. But you can pick some networking library to save your time
BUT its not over, its just the low level part. When you create a multiplayer game, you need to synchronize every important thing to the other client.

There is 1 problem, the enemy of most of multiplayer game developer. And the problem is latency. The moment when you play a multiplayer game, you can see something like 100ms in your screen, and that is the latency. Once your latency goes stonks (>200ms for example), the game starts to lagging. Then you see everything is jittery, your movement feels unresponsible. The game is unplayable

Fun fact: there is always lag on your game, you just cant see it if the latency is small (for example, 50ms)

### Can we hide lag?
Yes, you can. When i said "hide lag", i mean, hide the lag for the client so he still can play.

But how?
The main mission here is to hide the lag for the players. There are few steps to do this:
1. Client Prediction
Basically, we predict our movement before the server sends the position back to us.
2. Interpolation
Interpolation, we smooth the movement of every networked-entity
3. Lag Compensation/Server Rollback
Alright, from the name, it seems like we are going to decrease the latency. But no, that's not what we are going to do
So basically, we do some rollback so the client can shoot, even tho he is lagging. But this can result in a moment when 1 player is facing 1 other player. As soon as the second player is going behind the wall, he still dies. But keep in mind, thats just how lag compensation works.

These 3 are connected each other. Client prediction is for local player so the movement still responsive. Interpolation is for smoothing for every networked-entity. And lag compensation is helpful for shooting games, its for every networked-entity

### Data Compression
We can also try to reduce the data sent so the performance is going nicely.
How to do this? Simple, we do a snapshot compression. It sounds complicated, but no, its simple. To do this, we can drop some data and reconstruct it later

For example, we are making FPS game, we need to sync x axis for the local IK Rotation to look at, so its clear that we are aiming
We pack the data into a packet, we send all the quaternion axis, so the total is 4 floats. 1 float = 4 bytes, 4 floats = 4 * 4 = 16 bytes. We can reduce this by just looking at the localEulerAngles, pass the x part. So we are just sending 1 float

### Example game
You want an example on the implementation of these 3 (prediction, interpolation, and rollback/lag compensation) things on a game?
Take a look at CS 1.6 and CSGO! The netcode is nice, the game is responsive, so much good stuff on it
It has prediction, interpolation, and lag compensation

### Closing
All i can say is, keep strong when you create networking-related project.
I'll update this repo as soon as i found new useful thing

### Lists
1. https://www.codersblock.org/blog/client-side-prediction-in-unity-2018
2. https://www.gabrielgambetta.com/entity-interpolation.html
3. https://www.gabrielgambetta.com/lag-compensation.html
4. https://gafferongames.com/post/snapshot_compression/
