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


## :seedling: Interesting 42 Projects
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

### :sunny: [miniRT](https://github.com/fkernbac/miniRT)

>Team project:
>Write a program that renders images via raytracing.

*Team size: 2*  
*Language: C98*  

#### Mandatory Part:
* Libraries: miniLibX, a 42 C library for displaying images
* Geometric Objects: Implement at least three simple geometric objects - plane, sphere, and cylinder.
* Object Manipulation: Support resizing of objects and applying translation and rotation transformations.
* Lighting System: Implement spot brightness, hard shadows, and ambient lighting with ambient and diffuse components.
* Scene Description: Read scene details from a file with a .rt extension, specifying elements like ambient lighting, cameras, lights, spheres, planes, and cylinders.
As the mandatory requirements for this project are quite simple, we focused on the bonus part. With my background in 3D graphics I loved introducing soft shadows, stochastic sampling, multiple light sources and global illumination.

#### My Main Tasks:
I implemented the core raytracing algorithm, vector operations and color calculation.
* Color Correction: Enhanced the output image with color correction and color clamping. Implemented bounce color calculations and adjusted light intensity set in the input file.
* Progressive Sampling: Introduced an option for continuous rendering until the user decides to terminate the program. The raw color values of the image are persistently saved and updated with each iteration, while the displayed image in the window undergoes real-time color correction.
* Multi-Threading: Established thread routines with a focus on minimizing shared and duplicate memory.
* Documentation: Emphasized code readability by incorporating comments for functions and macros. It's something easily forgotten in school projects. I also _really_ like clear and self-explanatory names.
* Object Structures: Designed and initialized structures for vectors, rays, cameras, and threads. For the rays especially I tried to avoid any unnecessary recalculations.
* Optimization: I sped up our rendering algorithm by rearranging conditions and calculations. Unfortunately there wasn't enough time to implement my experiments with importance sampling and early ray termination.

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


