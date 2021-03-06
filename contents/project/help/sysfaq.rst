---
created: 2010-02-05 14:25
creator: pan
description: ''
title: 系统级问题
---
﻿==============================
系统级问题
==============================
.. Contents::
.. sectnum::


如果数据库损坏，所有文档数据会丢失？
==================================================

所有文档的存储，并不是在数据库中。而是采用简单存储策略，采用和系统相同的文件夹结构，直接存放在文件系统中。简单存储，数据不依赖任何软件，因为更加安全。

如果数据容量不断增长，系统能否平滑扩展？
=========================================================
1. 我们的数据在磁盘上的存储和网站上，目录结构完全相同  

我们称之为简单存储：数据不依赖软件的存在而存在，系统硬件能存多少，都能够满足。

2. 我们内部采用的是一个虚拟的文件系统，和实际数据存放位置有一个映射关系。未来如果扩容，调整这个配置文件即可。

大量用户，高并发响应的情况下，系统有没有采取相关的措施平滑应对？
=======================================================================
系统已经做了很多工作，提升并发处理的能力，包括：

1. 繁重任务(比如文档转换)异步进行，串行化，避免多人同时访问的时候，同时反复执行，导致系统假死；

2. 文件缓存，转换的文件、预览的图片，我们都采用文件缓存，这样系统访问的负载其实不大。

对高负载的情况，我们可以做负载均衡，多服务进程、多机提供服务。

系统是否安全，充分保证用户文档的安全性？
=============================================================
我们的系统提供了各种机制充分保证文档的安全性。包括

1. 提供严格的权限管理（委托管理、成组授权、权限继承、负授权、四层6级别查看人的权限），根据用户的不同等级、所属部门进行严格的权限划分，分别控制用户的文件查看、下载、上传、修改、复制、移动、删除、发布等权限，保证文档在使用过程中的安全。

2. 文档使用痕迹安全检视，对每一个文档、文件夹或者整个系统的所有操作都会记录进操作历史。一旦出现安全事故，管理员可进行追查，追溯问题源头，追究事故责任人。

3. 其他：包括支持Https安全传输、病毒扫描防护、回收站方式的安全删除等。

你们的系统是开源的吗？
=====================================
系统采用了大量优秀的开源产品和组件实现，站在巨人的肩膀上，易度能够提供更好的产品质量。

但易度文档管理系统目前不是开源的。我们也开放了部分代码回馈社区，主要是文件的查看器。即便不启动易度系统，使用文件查看器，也可以对易度数据进行完整的查看。

其他的文档管理系统，都需要额外采购很多附属软件，你们也需要吗？
================================================================

我们的系统是即装即用的，不需要任何其他第三方的收费软件。

其他的系统，往往需要额外安装MS Office、MS SQL Server、Adobe pdf等诸多软件才能真正使用，这样整体成本非常高。

而采用易度文档管理软件，由于采用大量的开源软件，因此能够做到费用最低。

对于autocad预览功能，如果您付费购买商业软件，可得到更好的预览效果。但这不是必须的。

.. _kkk:

采用开源软件，是否在不够安全？
=======================================
开源软件，一般是采用开放的模式，由全世界非常多的公司、个人联合起来共同开发的软件。每行代码都接受非常多人的审查，软件使用很广，测试充分，因此代码质量一般来说比封闭开发模式要高。

开源软件目前是政府的重点扶植项目，全国各地都有开源软件中心。包括中标、红旗等都是国内比较大型开源软件公司。目前润普也给文化部、解放军提供过开源解决方案和服务。美国、欧洲政府，以及联合国，目前都是以采购开源软件为主。google公司内部也是大量采用各种开源软件。

我们服务的很多客户，愿意采用开源软件，并不是因为成本低，而是因为质量好。

系统所要求的服务器性能如何
======================================
对服务器的要求，和您的公司使用人数有关系。

一般来说，对于50人以内的公司，普通的PC服务就可以了，比如双核至强CPU、2G内存这样的配置就已经足够了。


需要自己购买数据库吗？易度用的是什么数据库？
==================================================

不需要再购买数据库。

易度文档管理系统底层存储是采用润普自主开发的，并已经开源的FRS开放的文件存储系统 http://opensource.everydo.com/frs ；和Zope的对象数据库ZODB，我们用ZODB存储并非存储文档资料等核心数据，而是用以存储系统索引等信息。 

ZODB对象数据库，是更适合对内容数据的管理，ZODB和zope一起诞生，有悠久的历史，是python社区最成熟的对象数据库存储方案，拥有大量商业部署案例，可以支撑几千人的应用服务，很多大型的企业组织都在使用，例如：美国海军、ebay、迪斯尼、通用电气等。

.. _example:

易度在用户认证使用什么协议？支持与其它系统单点登录吗？
================================================================

用户认证，易度采用支持 CAS单点登录协议，可以和其他支持此协议的系统实现单点登录。包括常见的与Windows上的活动目录集成，LDAP集成等。 

CAS单点登录协议是美国耶鲁大学制定的一个单点登录协议，协议非常简单，被包括IBM等众多厂商接受。http://www.ja-sig.org/products/cas/
