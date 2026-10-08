# Lab 4 - Introduction to Docker

- **Course:** CST8915 - Full-stack Cloud-native Development
- **Student:** Kamal Krami (041273436)

## Demo Video

[Watch the Part 6 demo (Docker Compose) on YouTube](https://youtu.be/QRHmopQKPPU)

## Reflection Questions

### 1. What are the main differences between a Docker image and a Docker container?

A Docker image is a read-only template that has the app code and everything the app needs to run. A container is a running copy of an image, and Docker adds a thin writable layer on top of it. For example, I used one image (`my-python-app:v3`) to run three containers: `app1`, `app2`, and `app3`.

### 2. Explain how Docker's layered architecture improves efficiency.

Each instruction in a Dockerfile creates a layer, and Docker saves these layers in a cache. When I rebuilt my image without any changes, it took only 1.1 seconds instead of 12.3 seconds, because Docker reused the layers. When I changed only `app.py`, Docker rebuilt only the last step. Images can also share the same layers, so they use less disk space.

### 3. Why does each container get its own writable layer?

Each container gets its own writable layer, so the changes in one container do not affect the other containers or the image. In the lab, I created a file in `app1`, and it did not appear in `app2` or `app3`. Also, when I changed `app.py` in `app1`, `app2` still had the original file.

### 4. What are the benefits of using Docker Compose over running containers individually?

Docker Compose lets me define all the services of an app in one file. With one command (`docker compose up -d`), I started the web app and Redis together, with their network and volume. It is also easier to stop the app, check the logs, and scale a service, for example with `--scale web=3`.

## Notes

- Docker cannot remove a running container, so I stopped `my-nginx` again before I ran `docker rm`.
- Docker Compose showed a warning that `version` is obsolete. This did not cause any problem.

## References
- [Docker Build Cache](https://docs.docker.com/build/cache/)
- [Docker Compose Overview](https://docs.docker.com/compose/)
- [Docker Storage Drivers](https://docs.docker.com/engine/storage/drivers/)