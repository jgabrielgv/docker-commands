A bunch of commands taken from https://www.udemy.com/course/docker-and-docker-compose-hands-on-by-example/

Install Docker Toolbox for windows (my specific environment)
https://docs.bitnami.com/containers/how-to/install-docker-in-windows/

Open Docker Toolbox terminal

```
$ docker run hello-world
```

Docker Desktop vs Docker Toolbox

Be careful using docker desktop vs docker toolbox, meaning docker toolbox provides a specific IP address that you need to use when testing your apps. You should see this IP address when the terminal pops up at the beginning:

... docker is configured to use the default machine with IP 192.168.99.100 ...

Testing the IP address

Just create a simple Apache image using Docker Toolbox:

```
$ docker run --rm -p 8080:80 httpd
```

So instead of using http://localhost:8080, you need to access the actual IP address where the Apache server is running, which is http://192.168.99.100:8080 (in my case the IP address is http://192.168.99.100).

Hands On Commands

The command below allows you to install Ubuntu with a specific process attached (<code>/bin/bash</code>). This will automally leave the container running and open the ubuntu terminal (<code>-it</code> for interactive terminal) rather than your OS terminal:

```
$ docker run -it ubuntu /bin/bash
```

It's easy to test if the container works by following these simple commands:

```
root@3e54d12e12f1:/# cd /home/
root@3e54d12e12f1:/home# mkdir test-folder
root@3e54d12e12f1:/home# ls
test-folder
```

You can lookup the running containers by using <code>$ docker ps</code>. This will give you a list like this one:

```
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
3e54d12e12f1        ubuntu              "/bin/bash"          5 minutes ago       Up 5 minutes                               stoic_mahavira
```

So, if you exit from your linux container:

```
root@3e54d12e12f1:/home# exit
```

Then if you run <code>$ docker ps</code> again, the list from above should be empty now:

```
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                  NAMES
```

But if you run <code>$ docker ps -a</code> the console should present the entire list of containers, including those that are inactive:

```
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS                      PORTS                  NAMES
3e54d12e12f1        ubuntu              "/bin/bash"          15 minutes ago      Exited (0) 6 minutes ago                           stoic_mahavira
```

You can start the specific container by using the container Id (or just the initials) or the image name using <code>$ docker start 3e54</code>.

Going a step further, we can attach the image (to actually use the container), so the ubuntu terminal will be displayed using <code>$ docker attach 3e54</code>.

The container can be stopped using <code>$ docker stop 3e</code> from a second terminal, this automatically kills the container active session.

Finally, the container can be fully removed by running <code>$ docker rm stoic_mahavira</code>.