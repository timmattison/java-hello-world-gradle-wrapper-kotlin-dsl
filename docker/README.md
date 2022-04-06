# Minimal application in a Docker container

This is a minimal Hello World application that runs in a Docker container. It uses a build
container based on the latest OpenJDK Docker image from Dockerhub. This build container builds
the uber JAR and the custom runtime with JLink.

After the build container is built it creates a runner container. The runner container is a
minimal Debian container that contains the uber JAR and the custom runtime. The entry point for
the runner container immediately starts the uber JAR.

# Thanks to David Delabassee

I learned how to do this from [David Delabassee's "Java into Containers, A Match Made in Heaven?" video](https://www.youtube.com/watch?v=ikipIFv5S3I). It is definitely worth a watch if you want to know more about Java, Docker containers, Java Class Data Sharing (CDS), and JLink.

# To build and run the application

To build and run the application do this:

```
docker build -t hello-world-docker .
docker run -it --rm hello-world-docker
```

You should see this output:

```
Hello World!
```

# Beware! Alpine Linux is not supported (yet)

It is tempting to want to use a smaller container for the runner container. Alpine Linux is
usually a good choice for this. However, the OpenJDK latest container uses glibc and Alpine
Linux uses musl. If you try to use Alpine Linux you will get an error message that looks like
this:

```
standard_init_linux.go:228: exec user process caused: no such file or directory
```

If you go further down the rabbit hole and try to install `gcompat` to get glibc compatibility
you will likely get an error message like this:

```
Error occurred during initialization of VM
Unable to load jimage library: /custom-runtime/lib/libjimage.so
```
