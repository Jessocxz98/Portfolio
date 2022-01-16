# Week 1 Notes

## Containerisation with Docker
- Containerisation involves encapsulating or packaging up software code and all its dependencies so that it can run uniformly and consistently on any infrastructure. 
- Docker is an open source containerisation platform that allows you to containerise your applications, share them using public or private registries, and also to orchestrate them.
**Container**
- A container is an abstraction at the application layer that packages code and dependencies together. Instead of virtualizing the entire physical machine, containers virtualize the host operating system only.
- Just like virtual machines, containers are completely isolated environments from the host system as well as from each other. They are also a lot lighter than the traditional virtual machine, so a large number of containers can be run simultaneously without affecting the performance of the host system.
- Virtual machines are usually created and managed by a program known as a hypervisor. This hypervisor program usually sits between the host operating system and the virtual machines to act as a medium of communication. Each virtual machine comes with its own guest operating system which is just as heavy as the host operating system. The application running inside a virtual machine communicates with the guest operating system, which talks to the hypervisor, which then in turn talks to the host operating system to allocate necessary resources from the physical infrastructure to the running application. As you can see, there is a long chain of communication between applications running inside virtual machines and the physical infrastructure. The application running inside the virtual machine may take only a small amount of resources, but the guest operating system adds a noticeable overhead.
- Instead of having a complete guest operating system inside a container, a container just utilizes the host operating system via the container runtime while maintaining isolation – just like a traditional virtual machine. The container runtime, that is Docker, sits between the containers and the host operating system instead of a hypervisor. The containers then communicate with the container runtime which then communicates with the host operating system to get necessary resources from the physical infrastructure. 
- Containers virtualize the host operating system instead of having an operating system of their own.
**Image**
- Images are multi-layered self-contained files that act as the template for creating containers. They are like a frozen, read-only copy of a container. Images can be exchanged through registries. 
- Containers are just images in running state. When you obtain an image from the internet and run a container using that image, you essentially create another temporary writable layer on top of the previous read-only ones.
**Registry**
- An image registry is a centralized place where you can upload your images and can also download images created by others.
**Docker Archictechture**
- The engine consists of three major components
1. Docker Daemon: The daemon is a process that keeps running in the background and waits for commands from the client. The daemon is capable of managing various Docker objects.
2. Docker Client: The client is a command-line interface program mostly responsible for transporting commands issued by users.
3. REST API: The REST API acts as a bridge between the daemon and the client. Any command issued using the client passes through the API to finally reach the daemon.

### Running a Container
**Publishing a Port**
- Containers are isolated environments. Your host system doesn't know anything about what's going on inside a container. Hence, applications running inside a container remain inaccessible from the outside.
- To allow access from outside of a container, you must publish the appropriate port inside the container to a port on your local network.
**Using Detached Mode**
-  Normally, in order for the container to keep running, you have to keep the terminal window open. Closing the terminal window also stops the running container.
- This is because, by default, containers run in the foreground and attach themselves to the terminal like any other normal program invoked from the terminal.
- In order to override this behavior and keep a container running in background, you can include the --detach option with the run command.
- 

### Docker Cheat Sheet
- `docker --version`
- `docker-compose --version`
- `docker run image-name` finds image locally or pulls it from registry and runs as container (It's the default behavior of Docker daemon to look for images in the hub that are not present locally. But once an image has been fetched, it'll stay in the local cache. If there is a newer version of the image available on the public registry, the daemon will fetch the image again.)
- `docker <object> <command> <options>` Object indicates the type of Docker object you'll be manipulating. This can be a container, image, network or volume object. Command indicates the task to be carried out by the daemon, that is the run command. Options can be any valid parameter that can override the default behavior of the command. The order of the options you provide doesn't really matter. In the case of the run command the image name must come last. If you put anything after the image name then that'll be passed as an argument to the container entry-point
- `--publish host-port:container-port` For port mapping, can also use `-p`. Using 8080:80 means any request sent to port 8080 of your host system will be forwarded to port 80 inside the container. E.g. `docker container run --publish 8080:80 image-name`
- `--detach` Can also use `-d`. Used like `docker container run --detach --publish 8080:80 image-name`
- `docker container ls` lists all containers which are currently running
- `docker ps -a` or `docker container ls -a` Can use `--all`. Lists all containers which are currently running or have run in the past
- `ctrl + c` stops running container

## Resources
- history lesson on containers: https://blog.aquasec.com/a-brief-history-of-containers-from-1970s-chroot-to-docker-2016