---
title: kubernetes和Docker学习笔记
date: 2023-07-28 15:38:11
categories: 
- 软件算法
- 生信无关
tags: ['技术','个人成长']
hide: true
---
kubernetes和Docker学习笔记
<!-- more -->
# Kubernetes
Kubernetes 是一个可移植、可扩展的开源平台，用于管理容器化的工作负载和服务，可促进声明式配置和自动化。 [Kubernetes](https://kubernetes.io/zh-cn/docs/concepts/overview/) 拥有一个庞大且快速增长的生态，其服务、支持和工具的使用范围相当广泛。

Kubernetes 这个名字源于希腊语，意为“舵手”或“飞行员”。k8s 这个缩写是因为 k 和 s 之间有八个字符的关系。 

![](container_evolution.svg)

Kubernetes 是 Google 团队发起并维护的基于 Docker 的开源容器集群管理系统，它不仅支持常见的云平台，而且支持内部数据中心。建于 Docker 之上的 Kubernetes 可以构建一个容器的调度服务，其目的是让用户透过 Kubernetes 集群来进行云端容器集群的管理，而无需用户进行复杂的设置工作。系统会自动选取合适的工作节点来执行具体的容器集群调度处理工作。其核心概念是 Container Pod。一个 Pod 由一组工作于同一物理工作节点的容器构成。这些组容器拥有相同的网络命名空间、IP以及存储配额，也可以根据实际情况对每一个 Pod 进行端口映射。此外，Kubernetes 工作节点会由主系统进行管理，节点包含了能够运行 Docker 容器所用到的服务。

常用的kubectl命令如下：

~~~shell
kubectl create -f <filename> ：通过配置文件名或stdin创建一个集群资源对象，支持JSON和YAML格式的文件，如：kubectl create -f  deployment.yaml

kubectl get pods：获取具体命令空间下的任务情况，可获取pod号，如：kubectl get pods -n snakemake-scrna

kubectl describe pod <pod-name>：获取pod的详细信息

kubectl logs <pod-name>：获取pod的日志信息，如：kubectl logs  pods 2022-10-08-16-40-jg2022081232-faaggcia-j9bt6  -n  snakemake-scrna

kubectl exec -it <pod-name> /bin/bash：进入pod的shell环境，进行调试，如：kubectl exec -it -n snakemake-scrna  2023-03-22-09-10-2303200104-230320010494620-7gqx5  /bin/bash

kubectl delete -f <filename>：使用yaml文件删除资源，如kubectl delete -f deployment.yaml

kubectl delete jobs ：使用jobs号杀死任务，如：kubectl delete  jobs  2023-03-08-15-03-jg2022081232-dbifa  -n snakemake-scrna
~~~


# Docker
## 基本概念
Docker 包括三个基本概念：镜像（Image） 容器（Container） 仓库（Repository）。

1）镜像

镜像是Docker生命周期中的一个关键概念，它是一个只读的模板，用于创建Docker容器。镜像可以看作是一个打包好的软件，包含运行某个软件所需的所有内容，包括代码、运行环境、库文件、配置文件等。

2）容器

容器是Docker生命周期中的另一个关键概念，是由镜像创建的运行实例。一个镜像可以创建多个容器，容器之间是隔离的，相互之间不会有任何影响。

3）仓库

仓库是Docker生命周期中的另一个关键概念，用于存储和管理Docker镜像。可以将仓库看作是Docker镜像的集合，其中包含了所有版本的镜像，而每个镜像都有唯一的标识符。

[程序员进阶](https://it-blog-cn.com/blogs/container/docker_base.html#%E4%B8%80%E3%80%81%E7%AE%80%E4%BB%8B)

[Linux 101（中科大）](https://101.lug.ustc.edu.cn/)

## 镜像制作
