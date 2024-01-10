## Hello World!
I am a student of the 42 coding school in Heilbronn, Germany, and graduate of HDM Stuttgart with focus on 3D animation. I've mainly worked with _C, C++, TypeScript_ and _Docker_.

My hobbies include...
* :hocho:  historical european martial arts
* :pencil2:  digital painting and sketching
* :computer:  3D sculpting and animation
* :books:  ancient languages – latin, greek, egyptian
* :alien: video games
* :dog2: dogs

I'm hoping to learn...
* :snake: python
* :sparkles: 3D printing
* :herb: scottish gaelic


## :seedling: Main 42 Projects
### :tennis: [Transcendence](https://github.com/fkernbac/transcendence)
>Team project:
>create a pong contest website as single-page application.

*Team size: 4*  
*Backend Framework: NestJS (TypeScript)*  
*Frontend Framework: Vue.js (TypeScript)* 

#### My main tasks:

**Backend Game Logic:**  
A main difficulty was to differentiate the 3 different game modes + API game calls without introducing too much code duplication. Under no circumstances can a player be allowed to change the data of another player!

**Ball Collision:**  
In earlier versions the ball could pass through a paddle at high velocities because we relied on checking a hitbox area. I reworked our collision algorithm to calculate the intersection point with the edge of the playing field. It greatly reduced the angry yelling of our testers.

**Setup of WebSocket communication:**  
In our backend, GameGateway sends and receives all information related to games. Handling interrupted connections, asynchronous database calls and guarding against resulting empty objects kept me busy.

**Setup of a Basic Game API:**  
A game can be initalized, updated and the paddles be moved via API calls. The game logic needed to be modified by a surprising amount, because these games cannot be saved in our database.

**Two Factor Authentication:**  
The user can enable and disable 2FA on their profile with an authenticator app. A difficulty was managing the state between log in with password/OAuth and acceptance of the 2FA code. The JWT token for authentication is only sent to the frontend after the second step.

**TLS Encryption for HTTPS and WebSocket Connections:**  
I set up self-signed certificates and added authentication guards for all relevant calls to the backend. WebSocket connections that cannot provide a valid JWT token will be denied.

**Multiple Language Support:**  
I set up the translation in English, German and Italian for our frontend. Incorporation the vue.js plugin was done quickly, but saving the user's preferred language on the database, then calling and applying it after each login method without any bugs proved more complicated.

### :fork_and_knife: [Philosophers](https://github.com/fkernbac/philosophers)
> Multithreading project:
> solve the dining philosophers problem where each philosopher is a thread and their forks are represented by mutexes.

*Languages: C98*

As there are no *philosophers_bonus* projects available online which terminate without memory leaks when checked with valgrind, I was frequently asked by other students about this project. The secret is... never using kill() to quit a child process, and this requires additional threads in each process.

#### Main project:
To avoid a deadlock, all mutexes need to be locked in the same order. Because of this my last philosopher will frequently starve, because they got an extra rule to assure the their fork is always locked after the first one. I tried to solve this by making the philosophers count up: One of them will forgo their fork each turn, so that the last philosopher is not always the one without meal.  
I use a lot of mutexes to keep my program run fast, and wrote extra functions that handle their locking and unlocking. Otherwise the code becomes illegible quickly with loads of mutex unlocking inside and outside of conditional statements.

#### Bonus project: 
Each philosopher is a child process now, and the only communication between them is via semaphores. Each philosopher process contains a thread that does nothing but wait for the shutdown semaphore to open. Another thread in each philosopher process will monitor its own starvation and fullness status, and add enough resources to the shutdown semaphore so that each process will terminate. With this logic it is guaranteed that each thread frees its memory and exits by itself.


