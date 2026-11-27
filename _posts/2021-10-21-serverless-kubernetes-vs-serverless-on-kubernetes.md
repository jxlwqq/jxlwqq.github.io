---
layout: post
title: "Serverless Kubernetes 和 Serverless on Kubernetes 的区别"
date: 2021-10-21 14:59:00 +0800
categories: kubernetes serverless
---

### 什么是 Kubernetes？

Kubernetes 是一个可移植的、可扩展的开源平台，用于管理容器化的工作负载和服务，可促进声明式配置和自动化。

### 什么是 Serverless ？

无服务器是一种云原生开发模型，可使开发人员专注构建和运行应用，而无需管理服务器。

无服务器方案中仍然有服务器，但它们已从应用开发中抽离了出来。云服务提供者（如公有云服务商、组织内部的基础设施部门等）负责置备、维护和扩展服务器基础架构等例行工作。开发人员可以简单地将代码打包到容器中进行部署。

部署之后，无服务器应用即可响应需求，并根据需要自动扩容。公共云提供商的无服务器产品通常通过一种事件驱动执行模型来按需计量。因此，当无服务器功能闲置时，不会产生费用。

无服务器与其他云计算模型的区别在于，它是由云提供商负责管理云基础架构和应用扩展。无服务器应用部署在容器中，这些容器在被调用时会自动按需启动。

在标准的基础架构即服务（IaaS）云计算模型中，用户需要预先购买容量单元；也就是说，你要先向公共云提供商支付始终可用的服务器组件的费用，才能运行你的应用。  用户自行负责在需求高时扩展服务器容量，并在不再需要时缩减容量。即使在应用闲置不用期间，运行该应用所需的云基础架构也要保持就绪。

无服务器架构则与之相反，应用仅在需要时启动。有事件触发应用代码运行时，公共云提供商才会为这一代码分配资源。该代码执行结束后，用户便不再付费。除了成本与效率上的优势外，无服务器也能将开发人员从应用扩展和服务器置备相关的琐碎日常任务中解放出来。

使用无服务器时，管理操作系统和文件系统、安全补丁、负载平衡、容量管理、扩展、日志和监控等例行任务都由云服务提供商分担。

### 什么是 Serverless Kubernetes？

Serverless Kubernetes 也可以被称为 Nodeless Kubernetes，是一种特殊的 Kubernetes 集群。它的特殊之处在于：通过 Virtual Kubelet （虚拟 Kubelet）将 Serverless 服务作为 Kubernetes 集群的一个无限 Node 使用，这样就无需考虑 Node 数量的问题。

### 什么是 Serverless on Kubernetes？

作为一种在自动化基础架构中运行容器化应用的方式，Kubernetes 是运行无服务器环境的热门选择。然而，Kubernetes 本身并不足以原生运行无服务器应用。

Knative 是一个开源社区项目，可以添加组件，从而在 Kubernetes 上部署、运行和管理无服务器应用。

利用 Knative 无服务器环境，你可以将代码部署到 Kubernetes 平台。借助 Knative，可以将代码打包为容器镜像并交给系统，以此来创建相应的服务。代码仅在需要时才会运行，并由 Knative 来自动启动和停止实例。

### 什么是 Serverless on Serverless Kubernetes？

有意思的来了，你可以在一个 Serverless Kubernetes 集群中部署 Knative，从而构建一个无服务器环境吗？

答案当然是肯定的啦。这就是“Serverless on Serverless Kubernetes”。

### 参考

- [Serverless Kubernetes - 理想，现实与未来](https://developer.aliyun.com/article/754302)
- [Understand Serverless Kubernetes and Serverless on Kubernetes](https://www.youtube.com/watch?v=xL6lixC4D8Q)
- [Virtual Kubelet](https://virtual-kubelet.io/)
- [Knative](https://knative.dev/docs/)
