---
layout: post
title:  "一定要尽快解决vasp报错的问题！"
categories: work
tags:  vasp TPL  
author: FireCheng
---

* content
{:toc}
  
# vasp问题根源  
周四下午去了ITap的coffee break consultation，向他们请教了vasp报错的问题。经过一番排查，他们告诉我这是内存占用的问题。一个节点上的可用内存大概为90GB，而我提交的job在运行时一个core占用的内存就有十几G，因此内存溢出了。所以才会一直报出这种错误：  
```
vasp_std           0000000000414469  Unknown               Unknown  Unknown
forrtl: error (78): process killed (SIGTERM)
Image              PC                Routine            Line        Source
vasp_std           0000000000FC8AE4  for__signal_handl     Unknown  Unknown
libpthread-2.17.s  00002AD1AE08C5D0  Unknown               Unknown  Unknown
libmlx5.so.1.0.0   00002AD1B7772F80  Unknown               Unknown  Unknown
mca_btl_openib.so  00002AD1C143997B  Unknown               Unknown  Unknown
libopen-pal.so.20  00002AD1AFA01751  opal_progress         Unknown  Unknown
libmpi.so.20.10.3  00002AD1AE983AFE  ompi_request_defa     Unknown  Unknown
libmpi.so.20.10.3  00002AD1AE9CD6E3  ompi_coll_base_al     Unknown  Unknown
libmpi.so.20.10.3  00002AD1AE9957AA  PMPI_Allreduce        Unknown  Unknown
libmpi_mpifh.so.2  00002AD1AE71DBC9  mpi_allreduce_        Unknown  Unknown
vasp_std           00000000004151F0  Unknown               Unknown  Unknown
vasp_std           00000000006F0A57  Unknown               Unknown  Unknown
vasp_std           0000000000E0A9EB  Unknown               Unknown  Unknown
vasp_std           0000000000414562  Unknown               Unknown  Unknown
libc-2.17.so       00002AD1AEF723D5  __libc_start_main     Unknown  Unknown
vasp_std           0000000000414469  Unknown               Unknown  Unknown
forrtl: error (78): process killed (SIGTERM)
Image              PC                Routine            Line        Source
vasp_std           0000000000FC8AE4  for__signal_handl     Unknown  Unknown
libpthread-2.17.s  00002AC539AB45D0  Unknown               Unknown  Unknown
vasp_std           00000000004992BA  Unknown               Unknown  Unknown
vasp_std           0000000000E080D6  Unknown               Unknown  Unknown
vasp_std           0000000000414562  Unknown               Unknown  Unknown
libc-2.17.so       00002AC53A99A3D5  __libc_start_main     Unknown  Unknown
vasp_std           0000000000414469  Unknown               Unknown  Unknown
forrtl: error (78): process killed (SIGTERM)
Image              PC                Routine            Line        Source
vasp_std           0000000000FC8AE4  for__signal_handl     Unknown  Unknown
libpthread-2.17.s  00002AB919E755D0  Unknown               Unknown  Unknown
libopen-pal.so.20  00002AB91B7EA7E8  opal_progress         Unknown  Unknown
libmpi.so.20.10.3  00002AB91A76CAFE  ompi_request_defa     Unknown  Unknown
libmpi.so.20.10.3  00002AB91A7B66E3  ompi_coll_base_al     Unknown  Unknown
libmpi.so.20.10.3  00002AB91A77E7AA  PMPI_Allreduce        Unknown  Unknown
libmpi_mpifh.so.2  00002AB91A506BC9  mpi_allreduce_        Unknown  Unknown
vasp_std           00000000004151F0  Unknown               Unknown  Unknown
vasp_std           00000000006F0A57  Unknown               Unknown  Unknown
vasp_std           0000000000E0A9EB  Unknown               Unknown  Unknown
vasp_std           0000000000414562  Unknown               Unknown  Unknown
libc-2.17.so       00002AB91AD5B3D5  __libc_start_main     Unknown  Unknown
vasp_std           0000000000414469  Unknown               Unknown  Unknown

```  
既然清楚是内存占用过大的原因，那么解决方法也只有一个，想办法减小内存的占用量。我初步设想的具体办法有：  
1. 减小体系原子数。也就是扩胞的时候减小扩胞倍数；  
2. 减小K点数量。  
3. 占用多个节点，但只用部分核。这方法是consultation的人告诉我的，是否可行还有待验证。  
看来以后都不能算大体系了，唉。这种不可解决的问题真是烦。  

# 年会完整视频  
我在写这篇日记的同时，TPL年会也正在进行，今年去的衡山。唯唯负责今年的视频剪辑，剪的很好。附上链接[2019 TPL年会@衡山][1]  


[1]:https://www.bilibili.com/video/av80047238
  


