---
layout:     post
title:      【随笔】对UITableViewCell刷新造成核心动画丢失的问题记录
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

在UITableViewCell刷新时，即调用- (UITableViewCell*)tableView:(UITableView*)tableView cellForRowAtIndexPath:(NSIndexPath*)indexPath，刷新复用池中的cell时会造成之前给cell添加的核心动画失效。

#原因：

在从cell复用池中获取cell时，虽然获取到的cell与我们需要的cell是同一个，但是cell当中的核心动画会丢失，即使removedOnCompletion置NO也无效。

#解决策略：

针对特定的cell不采用系统的复用机制，而是增加一个属性对该cell进行保存，刷新cell时直接用该属性进行更新，并返回给TableView，这样动画就不会丢失了。

#弊端：

只能针对特定的cell处理，如果cell较多，不建议这种方式。
治标不治本。

