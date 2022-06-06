docker build --tag brentgroves/etl-pod:1 .
https://www.freecodecamp.org/news/docker-cache-tutorial/

How to Use Docker Arguments for Cache-Busting
Another option allows providing a little starting point in the Dockerfile. You need to edit your Dockerfile like this:

FROM nginx:1.21.6

# Update all packages
RUN apt-get update && apt-get -y upgrade

# Custom cache invalidation
ARG CACHEBUST=1

# Use a custom startpage
RUN echo '<html><bod>New Startpage</body></html>' > /usr/share/nginx/html/index.html


You add a CACHEBUST argument to your Dockerfile at the location you want to enforce a rebuild. Now, you can build the Docker image and provide an always different value that causes all following commands to rerun:

$ docker build -t my-custom-nginx --build-arg CACHEBUST=$(date +%s) .

=> [1/3] FROM docker.io/library/nginx:1.21.6@sha256:e1211ac1...    0.0s
=> CACHED [2/3] RUN apt-get update && apt-get -y upgrade           0.0s
=> [3/3] RUN echo '<html><bod>My Custom Startpage...               0.3s

=> exporting to image                                              0.0s
=> exporting layers                                                0.0s
=> writing image                                                   0.0s
=> naming to docker.io/library/my-custom-nginx

Building 1.0s (7/7) FINISHED
By providing --build-arg CACHEBUST=$(date +%s), you set the parameter to an always different value that causes all following layers to rebuild.

Summary
Docker’s build-cache is a handy feature. It speeds up Docker builds due to reusing previously created layers.

You can use the  --no-cache option to disable caching or use a custom Docker build argument to enforce rebuilding from a certain step.

Understanding the Docker build cache is powerful and will make you more efficient in building your Docker container.

I hope you enjoyed this article.

If you liked it and feel the need to give me a round of applause or just want to get in touch, follow me on Twitter.

I work at eBay Kleinanzeigen, one of the world’s biggest classified companies. By the way, we are hiring!

References
Docker arg instruction
Stackoverflow: Disable Cache for specific RUN commands
Baeldung: How the Docker Build Cache Works and When Not to Use it

Imagine, I have docker image based on Dockerfile, I will tag & push it into docker registry

Over time, I change Dockerfile (add/change new instructions, ...)

Now, I will tag new image again with the same tag I used in the first place and push it into docker registry

How does docker registry react to new layers?
How does docker registry react to changed layers?
Will it overwrite existing image with the latest version?
Should I use different tag to make sure I have correct new image in place?
docker
docker-registry
Share
Edit
Follow
Flag
asked Nov 14, 2016 at 16:31
user avatar
Patrik Mihalčin
2,65155 gold badges3131 silver badges5959 bronze badges
Add a comment
1 Answer
Sorted by:

Highest score (default)

10

How does docker registry react to new layers? How does docker registry react to changed layers?

It will function the same as a pull -- unchanged layers will not be pushed again and new layers will be pushed.

Will it overwrite existing image with the latest version?

Yep.

Should I use different tag to make sure I have correct new image in place?

Usually. Using latest to represent the most recent is fine but you should add a second tag for the actual version so that dependent systems can pin to that version and upgrade as needed.