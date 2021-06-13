
## Build
```bash
docker build --tag telegram:latest .

docker run -d --name td \
       --hostname=$(hostname) \
       -e DISPLAY=unix$DISPLAY \
       -e PULSE_SERVER=unix:$XDG_RUNTIME_DIR/pulse/native \
       -v /tmp/.X11-unix:/tmp/.X11-unix \
       -v "/home/$(whoami)/.Xauthority:/home/user/.Xauthority" \
       -v $XDG_RUNTIME_DIR/pulse:$XDG_RUNTIME_DIR/pulse \
       -v /etc/localtime:/etc/localtime:ro \
	   telegram:latest

docker start td
```

## Save the cotainer
```bash
docker container commit td telegram:con
docker rmi telegram:latest
# makes a new image based on the container (data inclded)
docker run -d --name td \
	--hostname=$(hostname) \
	-e DISPLAY=unix$DISPLAY \
	-e PULSE_SERVER=unix:$XDG_RUNTIME_DIR/pulse/native \
	-v /tmp/.X11-unix:/tmp/.X11-unix \
	-v "/home/$(whoami)/.Xauthority:/home/user/.Xauthority" \
	-v $XDG_RUNTIME_DIR/pulse:$XDG_RUNTIME_DIR/pulse \
	-v /etc/localtime:/etc/localtime:ro \
	telegram:con

docker image save telegram:con -o image.tar
docker image load -i image.tar
```