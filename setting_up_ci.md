# Github-Actions

## What is CI-CD?
An automated script which runs on the server and gives back the result. It can be used to deploy a release to other teams/clients, to run sanity checks when new changes to the codebase is done etc.

## Why CI-CD ??
Recently, there has been lot of versioning issues when sharing with teams and within teams as well due to the fact that lot of diverse work is going on and the team is getting bigger. This will also remove the laziness of running sanity checks before any important codebaes merges.

## Steps to setup CI-CD
Currently three runners are connected to github. So three runs can run simultaneously and if there are more runs, github will automatically queue it and run it when a runner is available.
A docker image has been created with all the necessary tools for our usecases. Details regarding the docker can be found [here](https://github.com/Mindgrove-Technologies/DockerSetup/tree/master/tool_setup). If any additional tools are required to be installed in the docker, please raise an issue in that repo.
NOTE: The docker doesn't support ssh cloning. So don't use repoman with docker. Run it outside docker.
The command to use docker is
```bash
docker_runner echo "Hello"
```

Follow the below steps to create a new CI-CD action.
1. Create a .github/workflow/{FILENAME}.yml in the master branch.
2. Create a branch from your working branch and create the same file created previously in the new branch.
3. Start editing the file with the commands. An example workflow file can be found [here](https://github.com/Mindgrove-Technologies/vision-soc/blob/master/.github/workflows/Release_verilog_generation.yml#L14).
4. Go to 'Actions' which is present in the repo's top bar and select your action present in the left. Select the drop down 'Run workflow', enter the necessary options, select the branch etc. and Wolaaah !!!

## Some tips when writing the workflow file:
1. When cloning dependencies using ssh, please don't forget to add the below command:
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/github_ci
```
2. There are multiple ways to trigger an action.
To trigger manually, use the below:
```bash
on:
  workflow_dispatch:
```
To trigger an action when a PR is created or updated:
```bash
on:
  pull_request:
    branches: [X1_dev]
    types: [opened, synchronize, reopened]
```
To trigger whenever a specific tag is created:
```bash
on:
  push:
    tags:
      - 'X1_v*'
```
To get inputs when triggering any manual action:
```bash
on:
  workflow_dispatch:
    inputs:
      tag:
        description: "Tag to deploy"
        required: true
        type: string
``` 
3. To use current date and time:
```bash
      - name: Setting up the environment
        run: |
          echo "CURRENT_DATETIME=$(date +'%Y_%m_%dT%H_%M')" >> $GITHUB_ENV  
```
The above will create an environment variable. It can be used like below:
```bash
 - name: Zipping up the verilog 
        run: |
          mkdir -p release/
          mkdir -p release/{{ env.CURRENT_DATETIME }}
```
4. A specific tool named 'yq' has been installed in all runners which helps in updating yaml easily. For example, let's say, the speific run needs 'num_harts' to be updated to '2':
```bash
yq -i '(.num_harts) = 2' sample_config/c64_multicore/core64.yaml
```
5. For creating releases, NAS has been connected to the runners which will host all the drops. Please check [here](https://github.com/Mindgrove-Technologies/vision-soc/blob/d45a454d511534da0bef17f99989e9b9398cadb9/.github/workflows/Release_verilog_generation.yml#L40-L66) to get idea on how to do it.

### Issues.
If any issues are faced, please create an issue in this repo tagging @Rohit/@Mouna/@Santhosh.
