# 东岳招新

每逢考试就要作死，谁都拦不住，还有大概一个小时就要去考国际经济法了，但是忽然想写一篇关于Docker的文章，从开始接触Docker到现在，也有大概两三个月的时间了，这段时间里比较多的时间花在了Docker和Golang上，有一些自己的看法。这篇文章不是介绍向，是随笔向，嗯。

## 东岳是谁？

东岳全名为：东岳网络工作室（Dongyue Studio），我们是交大校内优秀的技术团队，致力于成为交大校内最大的互联网人才成长平台，通过技术培训、一对一指导以及校内外的实战项目，帮助交大学子们在技术、设计、产品、运营等各方面迅速成长，在互联网领域拥有更好的未来。

## 团队介绍

不过最近在Docker之外，被一个叫做Hyper Container的东西吸引了。他们的主页是[www.hyper.sh](https://www.hyper.sh/)，是北京的一家创业公司的产品的样子。这家公司做的[hyperd](https://github.com/hyperhq/hyperd)是一个在虚拟机上运行Docker容器的东西，跟一般意义上的，在虚拟机上运行一个Docker Daemon然后再运行容器的概念不同。

<figure>
	<img src="http://gaocegege.com/images/docker/hyper.png" alt="hyper架构图" height="500" width="500">
	<figcaption>hyper架构图</figcaption>
</figure>

其实现在我也不是太理解他们做了什么事情，但是看架构图可以发现，跟Docker相比，他们有一点很大的不同，就是Daemon程序不是直接运行一个容器，而是先启一个Instance，也就是虚拟机，然后在这个虚拟机里运行一个Pod，嗯对，在他们的概念里Pod是一等公民，跟k8s的概念比较类似。所以看上去是加了一层抽象，就是Pod，然后之前k8s只是简单地把Pod做成了share一个network的namespace，但其实Pod与Pod之间，没有什么隔离的感觉在里面，只是用传统的容器隔离的方式。而hyper做的事情感觉就是加了一层虚拟机，使得Pod之间做了传统的虚机来做隔离，这样在别的Pod导致内核崩溃的时候，其他Pod还能继续服务。

他们提出的概念是：

>HyperContainer is a Hypervisor-agnostic Docker Runtime that allows you to run Docker images on any hypervisor (KVM, Xen, etc.).

通过他们自己实现的内核和一个start的服务，就可以在虚拟机里直接去根据Docker的Image来运行容器。也就是他们自己所说的`HyperContainer = Hypervisor + Kernel + Docker Image
`。

感觉概念挺有意思的，最开始是在知乎上一个[回答](https://www.zhihu.com/question/35412725/answer/101715150)上知道了这样一个东西，然后就去看了看，还没有深入地去了解，等到毕设做完有时间的话再去看看吧。

## 结

哦，还有十几分钟就要考试了，愿原力与我同在。
