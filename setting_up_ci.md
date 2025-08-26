# Github-Actions

## What is CI-CD?
An automated script which runs on the server and gives back the result. It can be used to deploy a release to other teams/clients, to run sanity checks when new changes to the codebase is done etc.

## Why CI-CD ??
Recently, there has been lot of versioning issues when sharing with teams and within teams as well due to the fact that lot of diverse work is going on and the team is getting bigger. This will also remove the laziness of running sanity checks before any important codebaes merges.

## Steps to setup CI-CD
Currently three runners are connected to github. So three runs can run simultaneously and if there are more runs, github will automatically queue it and run it when a runner is available.
A docker image has been created with all the necessary tools for our usecases. Details regarding the docker can be found 
