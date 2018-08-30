---
layout:     post
title:      对UITableViewCell刷新造成动画失效的问题记录
subtitle:   UITableViewCell 问题记录
date:       2018-06-07
author:     angBin
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - iOS
    - Obj-C
    - UITableViewCell
---


#现象：

在UITableViewCell刷新时，即调用- (UITableViewCell*)tableView:(UITableView*)tableView cellForRowAtIndexPath:(NSIndexPath*)indexPath;刷新cell时会造成之前给cell添加的动画失效。

#原因：

在从cell缓冲池中获取cell时，虽然获取到的cell与我们需要的cell是同一个地址，但是cell当中的动画会丢失。

#解决策略：

针对特定的cell不采用系统的复用机制，而是增加一个属性对该cell进行保存，刷新cell时直接对该属性进行更新，并返回给TableView，这样动画就不会丢失了。

#弊端：

只能针对特定的cell处理，如果cell较多，不建议这种方式。

