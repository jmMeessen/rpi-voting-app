#!/bin/sh

# Maven build the jar
docker build -t worker-builder -f Dockerfile-builder ./

# Copy the Jar locally to be used with the main Dockerfile 
docker cp $(docker run worker-builder):/code/worker-jar-with-dependencies.jar ./
