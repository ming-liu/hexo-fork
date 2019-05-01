---
title: vi
date: 2018-10-03 11:30:31
tags: vi vim
---



###### 1. 显示行数 ######
``` javascript
1> set number, set nu
2> set nonumber,set nonu
```
###### 1. 自动缩进 ######
``` javascript
1> set autoindent,set shiftwidth=2,缩写: set ai sw=2
2> >> 表示当前行增加一级缩进。
3> << 表示当前行减少一级缩进。
4> 5>> 表示当前行开始的5行，增加一级缩进;5<<表示减少。
5> set noai
```

:set autoindent
