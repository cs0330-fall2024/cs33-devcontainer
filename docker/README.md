# CS33 Docker

## Building Container

Change into the `docker` directory and run `./build-container`

This should only need to be run once, however, we may need you to rebuild the container during the semester if we have to update the docker image.

## Running Container

`./run-container` will start a shell in the container.

You can have multiple terminals open in the same container.

If you would like a terminal open in a new container, run `./run-container -f`

## Optional: Persistent Container

`./run-container` defaults to creating an ephemeral container, which automatically removes itself upon stopping.

The downside of this is that any custom packages that you install will be purged upon the next time you start the container.

Running `./run-container` with the `-p` flag will create a persistent container that only stops when you exit the environment.

Then running `./run-container -p` again will resume the paused container.
