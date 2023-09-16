# Dockers

## Creating a Docker Container

### Pulling a Docker Image

- For example let's pull Ubuntu Image:

```
docker pull ubuntu
```

- Then run a container on the basis of the image you pull:

```
docker run ubuntu
```

- Now docker is configured to run a single process.

- Want the container to be interactive then:

```
docker run -it ubuntu
```

- You'll get inside of the container now... and you can check the properties of it!

- Also we can check the running dockers:

```
docker ps
```

- You can also run the container the foreground forever and all of your process within it in the background:

```
docker run ubuntu tail -f /dev/null
```


