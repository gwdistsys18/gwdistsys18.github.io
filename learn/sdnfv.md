---
layout: page
title: SDN and NFV
permalink: /learn/sdnfv/
---

This topic area will teach you about the emerging networking technologies Software Defined Networking and Network Function Virtualization. You will learn how to manage a network using an SDN controller and how to build high performance network services with an NFV framework. Going in depth in this topic area will prepare you to contribute to the OpenNetVM NFV framework being built as an open source project here at GW.

> ** This topic is subject to change! **

Note: This topic area will be more research focused and less well defined than the others, plus it will take more time! The Beginner level only covers SDN, while the Intermediate level is focused on NFV.

> To achieve *Beginner Level* mastery of SDN you must complete:

  - [Video: Introduction to SDN](https://www.youtube.com/watch?v=DiChnu_PAzA) - 14 min
  - [Tutorial: Using the OpenDaylight SDN Controller with the Mininet Network Emulator](http://www.brianlinkletter.com/using-the-opendaylight-sdn-controller-with-the-mininet-network-emulator/) - 1.5 hours?

> To achieve *Intermediate Level* mastery of SDN/NFV you must also complete the following:

The need for Fast I/O:
  - [Video: OpenNetVM NFV platform](https://www.youtube.com/watch?v=7FoZywcxbYg) - 30 min or [read the paper](http://faculty.cs.gwu.edu/timwood/papers/16-HotMiddlebox-onvm.pdf) (some of this was covered in the NFV lecture in class)
  - Video: Netmap - a framework for fast I/O: [Usenix Conference (30 min)](https://www.youtube.com/watch?v=la5kzNhqhGs) or [Google Tech Talk (60 min)](https://www.youtube.com/watch?v=SPtoXNW9yEQ) or [read the paper](https://www.usenix.org/system/files/conference/atc12/atc12-final186.pdf)

DPDK and OpenNetVM:
  - For these tasks you will need access to servers on [NSF CloudLab](https://cloudlab.us). Go to the website and create an account, listing "GWCloudLab" as the project you want to join. *I will need to approve your account before you can use it.*
  - To complete these tasks you will need to read through the [documentation for DPDK](https://doc.dpdk.org/guides/index.html). It provides a lot of information and much of it is very good. Nevertheless, it can be very overwhelming! You may have more success in this topic area if you work through this together with another student. You should also post to piazza about any questions you have.
    - Do not mindlessly follow the instructions -- be sure you understand what is happening!
  - [Install DPDK](https://doc.dpdk.org/guides/linux_gsg/index.html) and run the `skeleton` sample application - 180 mins
    - [Read the Docs](https://doc.dpdk.org/guides/sample_app_ug/skeleton.html) to understand how it works
  - Pick a section in the [Programmers Guide](https://doc.dpdk.org/guides/prog_guide/index.html) to learn about - 150 min
    - You must pick a different section than other students - use Piazza to claim your section
    - Write an explanation of the section you studied that would help a new user learn about it
  - [Install OpenNetVM](https://github.com/sdnfv/openNetVM/blob/develop/docs/Install.md) and run the Speed Tester and Bridge NFs - 120 min
  - Complete one of the "Good First Issue" bugs/feature requests in the [Issue Tracker](https://github.com/sdnfv/openNetVM/issues) - 120 min
