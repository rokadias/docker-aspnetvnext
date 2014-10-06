Aspnet Vnext Docker Image
==================

* This repository hosts the Dockerfile used to create the image at [https://registry.hub.docker.com/u/rokadias/aspnetvnext/]. Compared to other aspnetvnext docker images this does not include samples to run and expects those files to be outside of the docker image.

* This is built from the aspnet vnext dev branch so still very much in the experimental stage.

* Builds the mono 3.8.0 version since 3.10.0 at the point this image was created was not stable enough. 

# Getting Docker image of aspnetvnext
* Pulling the image
  `docker pull rokadias/aspnetvnext`
* or clone repository and build docker image
  `git clone https://github.com/rokadias/docker-aspnetvnext.git ~/docker-aspnetvnext`
  `cd ~/docker-aspnetvnext`
  `docker build --tag rokadias/aspnetvnext .`

# Getting source code for running with aspnetvnext (Optional)
This is optional in case you would like to use as sample aspnet site.
  ```
  mkdir ~/aspnet
  cd ~/aspnet
  git clone https://github.com/davidfowl/HelloWorldVNext.git
  cd HelloWorldVNext/src
  ln -s helloworldweb web
  ```

The last bit is to make sure there is a folder under the root of the project to /src/web that represents what website to run. Feel free to do the same with any of the samples under [https://github.com/aspnet/Home].

# Running a container with the image and source code available.
* Interactively running the image
  `docker run -itp 80:5000 --rm -v ~/aspnet/HelloWorldVNext:/var/aspnet rokadias/aspnetvnext`
* Detached running the image
  `docker run -ditp 80:5000 -v ~/aspnet/HelloWorldVNext:/var/aspnet rokadias/aspnetvnext`

* Port 5000 is used from david fowler's sample and is being remapped to port 80 on localhost this is based on the source code being used.
* The entry point will run `kpm restore` on the base of volume being attached and will then run k web on the src/web directory within that volume. That is why a symbolic link was created above.