[Understanding Docker Volumes - Earthly Blog](https://earthly.dev/blog/docker-volumes/#:~:text=Volumes%20can%20be%20declared%20in,it%20to%20the%20specified%20path.)

[Docker Basics: How to Use Dockerfiles - The New Stack](https://thenewstack.io/docker-basics-how-to-use-dockerfiles/)

# Test nginx web server

First, create a Dockerfile in any directory and modify the contents with VS code.

```bash
mkdir nginx
code Dockerfile

# place the following into Dockerfile
	FROM nginx:alpine
	COPY index.html /usr/share/nginx/html/index.html
```

Then, build & run the new image:
```docker
# build it
docker build -t ant13277/centos .   # (last part is %username% / %repository%)

# run it
docker run --rm --name nginx -it -d -p 3000:80 simple-nginx
```

```bash
# place the following into Dockerfile
	FROM centos:7
	MAINTAINER NAME EMAIL
	RUN yum makecache
	RUN yum upgrade -y
	RUN yum install -y httpd

# save & close


```

Now you can test it:
http://localhost:3000

Finally, you can ssh into the container:
```docker
sudo docker exec –it nginx-test /bin/bash
```