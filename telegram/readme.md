
# Build

```bash
# Create a new telegram image based on the Dockerfile 
docker build --tag telegram:latest ./

# Creating a new container from the image
docker run -d --name tc \
 --hostname=$(hostname) \
 -e DISPLAY=unix$DISPLAY \
 -e PULSE_SERVER=unix:$XDG_RUNTIME_DIR/pulse/native \
 -v /tmp/.X11-unix:/tmp/.X11-unix \
 -v "/home/$(whoami)/.Xauthority:/home/user/.Xauthority" \
 -v $XDG_RUNTIME_DIR/pulse:$XDG_RUNTIME_DIR/pulse \
 -v /etc/localtime:/etc/localtime:ro \
 telegram:latest

# Stopping and starting the container
docker stop tc
docker start tc
```

# Change the container and create a new image

Now we can change something in the container.

```bash
docker exec -ti -u root tc bash
touch hi
```

And create a new image

```bash
docker container commit tc telegram:newtag
# Remove the original image
docker rmi -f telegram:latest
# Save the new image
docker image save telegram:newtag -o image.tar
docker image load -i image.tar
```

Create a new container from the new image

```bash
docker run -d --name tcnew \
 --hostname=$(hostname) \
 -e DISPLAY=unix$DISPLAY \
 -e PULSE_SERVER=unix:$XDG_RUNTIME_DIR/pulse/native \
 -v /tmp/.X11-unix:/tmp/.X11-unix \
 -v "/home/$(whoami)/.Xauthority:/home/user/.Xauthority" \
 -v $XDG_RUNTIME_DIR/pulse:$XDG_RUNTIME_DIR/pulse \
 -v /etc/localtime:/etc/localtime:ro \
 telegram:newtag

# You can find the 'hi' file you created in the container 
docker exec -ti -u root tcnew bash
root@user:~# ls
# hi
```
