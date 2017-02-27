---
title: NaoController deployment with webpy
date: 2016-05-25
updated: 2016-05-26
type: "tags"
tags:
- nao
- app
---


**Nao robot** , is deployed on a Centoo-based operation system "***Naoqi***", with a dozen of softwares giving him human-like emotion. To get a convenient way to control nao, we write a Controller for him. Now, let us see how to do that with ***python*** and ***webpy***. 

<!--more-->

To get it convenient to make Nao move and interact with other people, we need to crate a easy-use application, where we can access from many other device. So I chose to make it a web server deployed on Nao's Head, so that I can access it once the robot operation is running.

First, I need a web struct. After comparing some most-used web server structure, I chose **webpy**, cause its simply development. 

Then, I deployed the server on Nao's operation device. And add the service to auto startup list, so that it can auto run once the robot start its service.
