# Adaptus Technology log

## Active Topics

# General journal

## docker restarting in amazon linux
*2022-12-12*

`sudo service docker restart`

https://forums.docker.com/t/failure-to-start-docker-on-an-amazon-linux-machine/44003

## Trying to use the latest aws linux 2022 with docker and docker compose v2
*2022-12-09*

https://stackoverflow.com/questions/70358656/rhel8-fedora-yum-dns-causes-cannot-download-repodata-repomd-xml-for-docker-ce

## Architectural Decision Records
*2022-11-16*

I've been trying to decide the right way to document architectural considerations and decisions and stumbled across some thought in this area.
There are top level statements that fit into how I document systems. See (https://adr.github.io/). In particular, the Y-statement (short form):

> In the context of `<use case/user story u>`, facing `<concern c>` we decided for `<option o>` to achieve `<quality q>`, accepting `<downside d>`.

And the long form:

> In the context of `<use case/user story u>`,  
> facing `<concern c>`  
> we decided for `<option o>` and  
> neglected `<other options>`,  
> to achieve `<system qualities/desired consequences>`,  
> accepting `<downside d/undesired consequences>`,  
> because `<additional rationale>`.

## sysbox
*2022-11-16*

I've been investigating how to update the both the provisioning/update system and create an on-demand worker mechanism. Stability for the provisioning system would improve with on-demand worker execution. On-demand workers are also key to unifying the cli execution with the running of framework and the production system.

There is a question of docker-out-of-docker between docker-in-docker. Using the host's docker works on top of ec2 nodes, but has a privilege issue. It also does not work if the framework is deployed on ecs or eks or kubernetes in general. Allowing docker-in-docker would allow a consistent mechanism whether running on hosts or on kubernetes.
