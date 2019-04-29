# Docker

---

What is a container? 

------

A container is simply a way to bundle together state change on a computer, and a way to isolate resources on a computer. 

------

It's kind of like a VM but it's definitely not a VM. 

---

Analogy Time

------

Computer/Server is like a City, it provides infrastructure (Water/Sewer/Electricity) for everyone. 

------

VM's are like Houses they each use City Infrastructure but manage it themselves. 

------

Containers are like Apartments, they don't manage their own infrastructure but let the Apartment (Docker Daemon) manage it for them .

------

Listen I know it's not perfect but it's the best I got right now. 


And I'm not the first person to come up with this analogy. 

- https://www.settlersoman.com/vms-are-houses-containers-are-apartments/
- https://blog.docker.com/2016/03/containers-are-not-vms/

I'm sure we can find others, but I'm not going to. 

---

Benefits of containers over VMs

- They start faster 
- They are (should) be immutable
- Configuration Management built in
    - No more works on my machine Dev/Test is identical to Production.

------

Cons of Containers over VMs

- Shared Host OS Kernel, you break into it one container you probably have access to everything. 

Note: Does this mean we shouldn't use Containers? Nope, just means you shouldn't act as if you are secure just because you are using them.


---

Okay, now that I have that awkward attempt to explain this out of the way let's get on with it. 

---

The Basics

---

Dockerfile  

Note: A file that has the instructions for building the docker file

---

Image 

Note: The results of the file that is built, not a file but usually a collection of files. You almost never interact with this directly on your filesystem. 

---

Registry 

Note: A website that has docker images that you can use to run applications, extend to run your own applications, and share your work with others. 


------

Public Registries

- Docker Hub
- Quay.io

Note: hub.docker.com is the most common public registry, Quay.io set managed keys per repo.

------

Private Regsitries

Note: you can host your own or use a managed registry through your CSP.

---

Layers

Note: Docker Images are built up of layers each layer corresponds to a line in a docker file.

---

Most Common Keywords 

------


`FROM` 

Note: First line in every file delineates the base layer, multi-stage docker containers can have multiple.


------

`COPY` 

Note: Copy from host os or previous stage to container/current stage

------

`RUN` 

Note: Run a shell command in the container 

------

`ENV`

Note: Set an environment variable in the container 


------

`EXPOSE`

Note: Expose an internal container port to the external os

------

`CMD`

Note: The command to be run when the container is run

------

`ADD`

Note: Download a file from the internet or copy from the host os into the container, invalidates cache afterwards

------

`ENTRYPOINT`

Note: lets you run a container as a single command 

---

Okay that's pretty much all the commands, there are a few others you can find the reference at: 

https://docs.docker.com/engine/reference/builder/

---

Docker Compose 

------

A way to run multiple docker containers together, great for hosting locally if you don't have something such as MiniKube or a local kubernetes instance. 

------

I'm not going to go into detail but with this one. 

