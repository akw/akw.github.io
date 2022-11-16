# Adaptus Technology log

## Active Topics

# General journal

## sysbox
*2022-11-16*

I've been investigating how to update the both the provisioning/update system and create an on-demand worker mechanism. Stability for the provisioning system would improve with on-demand worker execution. On-demand workers are also key to unifying the cli execution with the running of framework and the production system.

There is a question of docker-out-of-docker between docker-in-docker. Using the host's docker works on top of ec2 nodes, but has a privilege issue. It also does not work if the framework is deployed on ecs or eks or kubernetes in general. Allowing docker-in-docker would allow a consistent mechanism whether running on hosts or on kubernetes.
